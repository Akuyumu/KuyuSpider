---
tags:
  - y2s3-MnT
status: Ongoing
---
# Hello!
Read on to explore the block diagram made to simplify circuitry planning and logistics in the early stages of making the project.
[[Circuit_block_diagram.excalidraw|Excalidraw Link]]

## The Diagram
![[Circuit_block_diagram.excalidraw.png]]

*Power supply edited to be two 400mAh batteries*
## Details
### Hand mounted system
- [[I2C]] communication with [[MAX30102 - SpO2 & HeartRate]] 
- GY-MAX30102 is used for easy implementation
	- Integrated LED drivers allows a single 3.3V supply
- Investigate: Sensor on wrist or finger
- [[Adafruit Feather nRF52840 Sense]] communicates this data to user's phone via [[Bluetooth Low Energy (BLE)]]
### The code

``` C++
#include <Arduino.h>
#include <Wire.h> // I2C library
#include "Adafruit_TinyUSB.h"
#include <Adafruit_NeoPixel.h> // Neopixel LED library
#include <MAX30105.h> // MAX30105 or MAx30102 library
#include <spo2_algorithm.h> //SpO2 Sensor library

#define VBATPIN A6 // Battery voltage analog pin
#define NEOPIXELPIN 8 // Neopixel control pin
#define NUMPIXELS 1 // Number of neopixels
#define MAX_BRIGHTNESS 255 // for MAX30102

// Put variable declaration here
float VBat;

uint32_t irBuffer[100]; //infrared LED sensor data
uint32_t redBuffer[100];  //red LED sensor data

int32_t bufferLength = 100; //data length
int32_t spo2; //SPO2 value
int8_t validSPO2; //indicator to show if the SPO2 calculation is valid
int32_t heartRate; //heart rate value
int8_t validHeartRate; //indicator to show if the heart rate calculation is valid

// Put function declaration here
float getBattVoltage(int x);
void VBatIndicator();
void FillSensorBuffer();

// Initialize NeoPixel
Adafruit_NeoPixel pixel = Adafruit_NeoPixel(NUMPIXELS, NEOPIXELPIN, NEO_GRB + NEO_KHZ800);

//Initialise MAX30102 SpO2 Sensor
MAX30105 particleSensor;

void setup() {
  // put your setup code here, to run once:

  // Initialize NeoPixel
  pixel.begin();
  pixel.setBrightness(20); // Set brightness (0-255)
  pixel.show(); // Initialize all pixels to 'off'

  // Start Serial
  Serial.begin(115200);
  Serial.println("Outputting readings... NOW");

  Wire.begin(); // Initialize I2C

  // Initialize MAX30102
  if (!particleSensor.begin(Wire, I2C_SPEED_FAST)) {
    Serial.println("MAX30102 not found! Check wiring.");
    while (1); // Halt if sensor not found
  }

  Serial.println(F("Attach sensor to finger with rubber band. Press any key to start conversion"));
  while (Serial.available() == 0) ; //wait until user presses a key
  Serial.read();

  // Configure sensor for SpO2 monitoring
  particleSensor.setup(60, 4, 2, 100, 411, 4096); 
  /*
  Parameters: 
  LED brightness (0-255)
  Sample averaging (1, 2, 4, 8, 16, 32)
  LED mode (1 = Red, 2 = Red + IR)
  Sample rate (50, 100, 200, 400, 800, 1000, 1600, 3200)
  Pulse width (69, 118, 215, 411)
  ADC range (2048, 4096, 8192, 16384)
  */
}

void loop() {
  // put your main code here, to run repeatedly
  // Sequence to indicate battery status
  VBat =  getBattVoltage(analogRead(VBATPIN)); 
  VBatIndicator();
  Serial.println("hello i'm running");
  
  //read the first 100 samples, and determine the signal range
  static bool bufferfill = false;
  if (!bufferfill) {
      FillSensorBuffer();
      maxim_heart_rate_and_oxygen_saturation(irBuffer, bufferLength, redBuffer, &spo2, &validSPO2, &heartRate, &validHeartRate);
      bufferfill = true;
  }
  //dumping the first 25 sets of samples in the memory and shift the last 75 sets of samples to the top
  for (byte i = 25; i < 100; i++)
    {
      redBuffer[i - 25] = redBuffer[i];
      irBuffer[i - 25] = irBuffer[i];
    }

  //take 25 sets of samples before calculating the heart rate.
  for (byte i = 75; i < 100; i++)
  {
    while (particleSensor.available() == false) //do we have new data?
      particleSensor.check(); //Check the sensor for new data

    redBuffer[i] = particleSensor.getRed();
    irBuffer[i] = particleSensor.getIR();
    particleSensor.nextSample(); //We're finished with this sample so move to next sample

    //send samples and calculation result to terminal program through UART
    Serial.print(F("red="));
    Serial.print(redBuffer[i], DEC);
    Serial.print(F(", ir="));
    Serial.print(irBuffer[i], DEC);

    Serial.print(F(", HR="));
    Serial.print(heartRate, DEC);

    Serial.print(F(", HRvalid="));
    Serial.print(validHeartRate, DEC);

    Serial.print(F(", SPO2="));
    Serial.print(spo2, DEC);

    Serial.print(F(", SPO2Valid="));
    Serial.println(validSPO2, DEC);
    }

    //After gathering 25 new samples recalculate HR and SP02
    maxim_heart_rate_and_oxygen_saturation(irBuffer, bufferLength, redBuffer, &spo2, &validSPO2, &heartRate, &validHeartRate);
}

// put function definitions here
float getBattVoltage(int x) {
  float voltage = (x * 2 * 3.6) / 1024.0; 
  return constrain(voltage, 0.0, 4.2);  // LiPo max voltage is 4.2V

}

void VBatIndicator() {
    if (VBat > 4.1) {
    pixel.setPixelColor(0, pixel.Color(0, 255, 0)); // Green indicate full batt
  }
  else if (VBat < 3.4) {
    pixel.setPixelColor(0, pixel.Color(255, 0, 0)); // Red indicate low batt
  }
  else {
    pixel.setPixelColor(0, pixel.Color(0, 0, 255)); // Blue indicate otherwise
  }
  pixel.show();  // Call show() only once after setting the color
}

void FillSensorBuffer() {
  //read the first 100 samples, and determine the signal range
  Serial.println("Collecting samples...");
  //finger detection
  if (particleSensor.getIR() < 7000) {
      Serial.println("No finger detected");
      return;
  }
  for (byte i = 0 ; i < bufferLength ; i++)
  {
    while (particleSensor.available() == false) //do we have new data?
      particleSensor.check(); //Check the sensor for new data

    redBuffer[i] = particleSensor.getRed();
    irBuffer[i] = particleSensor.getIR();
    particleSensor.nextSample(); //We're finished with this sample so move to next sample

    // Print progress
    if (i % 10 == 0) {  // Print every 10th sample
      Serial.print("Progress: ");
      Serial.print(i);
      Serial.println("%");
    }
  }
  Serial.println("Samples Collected!");
}
```
### Chest mounted system
- Stretch of lower rib cage during breathing stretches [[Adafruit Conductive Rubber Sheet]], increasing it's resistance, creating a potential difference across a potential divider
- This P.D. is theoretically related to the stretch and thus related to the breath quantity
- This data will be calibrated to accurately represent the user's breathing via calibration in app, normalising the P.D. to the fully exhaled data and fully inhaled data
- The [[Adafruit Feather nRF52840 Sense]] reads this data and sends this data together with sound and motion data from its inbuilt sound sensor and accelerometer to the user's phone via [[Bluetooth Low Energy (BLE)]], UART communication protocol
### The Code

```C++
#include <Arduino.h>
#include <Adafruit_NeoPixel.h> // NeoPixel LED library
#include "Adafruit_TinyUSB.h" 
#include <bluefruit.h>
#include <PDM.h>
#include <arduinoFFT.h>
#include <Adafruit_LSM6DS33.h>

#define VBATPIN A6 // Battery voltage analog pin
#define NEOPIXELPIN 8 // Neopixel control pin
#define NUMPIXELS 1 // Number of neopixels
#define FFTSAMPLES 256 // Fast Fourier Transform sample collection
#define FFTSAMPLING_FREQ 16000
#define WHEATBRIDGEPIN_A A3 
#define WHEATBRIDGEPIN_B A4

// Put variable declaration here
float VBat; // Voltage of battery
int32_t mic; 
float dominantFreq;

extern PDMClass PDM;
short PDMsampleBuffer[256];  // buffer to read PDMsamples into, each sample is 16-bits
volatile int PDMsamplesRead; // number of PDMsamples read

double vReal[FFTSAMPLES];
double vImag[FFTSAMPLES];

Adafruit_LSM6DS33 lsm6ds33;
const float ALPHA = 0.95;  // Low-pass filter coefficient (Higher values (closer to 1) mean slower gravity filtering but better noise reduction)
float gravityX = 0, gravityY = 0, gravityZ = 0;        // Filtered gravity components
float lastAccelX = 0, lastAccelY = 0, lastAccelZ = 0;  // Previous acceleration readings
float deltaX = 0, deltaY = 0, deltaZ = 0;              // Change in acceleration

/* Create FFT object */
ArduinoFFT<double> FFT = ArduinoFFT<double>(vReal, vImag, FFTSAMPLES, FFTSAMPLING_FREQ);

// BLE Service for Environmental Sensing
BLEService        envService("181A");  // Environmental Sensing BLE service
BLECharacteristic soundChar("2A71", BLERead | BLENotify);    // Sound level
BLECharacteristic freqChar("2A76", BLERead | BLENotify);     // Frequency
BLECharacteristic accelChar("2A73", BLERead | BLENotify);    // Acceleration
BLECharacteristic stretchChar("2A77", BLERead | BLENotify);  // Custom for stretch
BLEUart bleuart;

// Put your function declarations here
float getBattVoltage(int x);
void VBatIndicator();
float computeFFT();
float getFilteredAcceleration();
float getPotDiffWheat();
void setupBLE();

int32_t getPDMwave(int32_t samples);
void onPDMdata();

// Initialize NeoPixel
Adafruit_NeoPixel pixel = Adafruit_NeoPixel(NUMPIXELS, NEOPIXELPIN, NEO_GRB + NEO_KHZ800);

void setup() {
    // Put your code here to run once at setup

    // Initialize NeoPixel
    pixel.begin();
    pixel.setBrightness(2); // Set brightness (0-255)

    // Quick test of NeoPixel
    pixel.setPixelColor(0, pixel.Color(255, 0, 0));  // Red
    pixel.show();
    delay(500);
    pixel.setPixelColor(0, pixel.Color(0, 255, 0));  // Green
    pixel.show();
    delay(500);
    pixel.setPixelColor(0, pixel.Color(0, 0, 255));  // Blue
    pixel.show();
    delay(500);
    pixel.setPixelColor(0, pixel.Color(0, 0, 0));  // Blue
    pixel.show();
    delay(500);

    // Start Serial
    Serial.begin(115200);
    Serial.println("Sensors outputting information... NOW!");

    // Setup BLE
    setupBLE();
    Serial.println("Advertising BLE...");

    // Start Accelerometer
    lsm6ds33.begin_I2C();
    // configure accelerometer for cough detection
    lsm6ds33.setAccelRange(LSM6DS_ACCEL_RANGE_4_G);
    lsm6ds33.setAccelDataRate(LSM6DS_RATE_104_HZ);
    // Initialize gravity filter with first reading
    sensors_event_t accel;
    sensors_event_t gyro;
    sensors_event_t temp;
    lsm6ds33.getEvent(&accel, &gyro, &temp);
    gravityX = accel.acceleration.x;
    gravityY = accel.acceleration.y;
    gravityZ = accel.acceleration.z;

    // Start sound sensor
    PDM.onReceive(onPDMdata);
    PDM.begin(1, 16000);
}

void loop() {
    // Put your code here to loop

    // indicate battery level
    VBat =  getBattVoltage(analogRead(VBATPIN)); 
    VBatIndicator();

    // Get sound sensor data
    PDMsamplesRead = 0;
    mic = getPDMwave(FFTSAMPLES);

    // Copy samples to FFT arrays only after we have enough data
    for (int i = 0; i < FFTSAMPLES; i++) {
        vReal[i] = (double)PDMsampleBuffer[i];
        vImag[i] = 0.0;
    }
    // Compute FFT and get dominant frequency
    dominantFreq = computeFFT();

    // Get Jerk movement data
    float acceleration = getFilteredAcceleration();

    // Compute potential diff across wheat bridge
    float PotDiff = getPotDiffWheat();

    // Print data
    Serial.print("RMS amplitude: ");
    Serial.print(mic);
    Serial.print("  Dominant frequency: ");
    Serial.print(dominantFreq);
    Serial.print(" Hz  Jerking: ");
    Serial.print(acceleration);
    Serial.print(" m/s²  Stretch Coeff (P.D.): ");
    Serial.print(PotDiff);
    Serial.println("V");
    // Optional: Only print when significant movement detected
    if (acceleration > 2.0) {  // Threshold for significant movement
        Serial.println("*** Significant movement detected! ***");
    }

    // Send data over BLE
    if (Bluefruit.connected()) {

        // FOR ENVIRO SERVICE

        // Convert float values to byte arrays for BLE transmission
        uint8_t soundData[4], freqData[4], accelData[4], stretchData[4];
        memcpy(soundData, &mic, 4);
        memcpy(freqData, &dominantFreq, 4);
        memcpy(accelData, &acceleration, 4);
        memcpy(stretchData, &PotDiff, 4);
        
        // Send notifications
        soundChar.notify(soundData, 4);
        freqChar.notify(freqData, 4);
        accelChar.notify(accelData, 4);
        stretchChar.notify(stretchData, 4);

        // FOR UART

        // Format data string exactly like Serial Monitor
        char uartData[150];  // Increased buffer size to prevent overflow
        memset(uartData, 0, sizeof(uartData));  // Clear buffer

        // Split the data into multiple transmissions to ensure reliable transfer
        sprintf(uartData, "RMS amplitude: %d\n", (int)(mic));
        bleuart.write(uartData, strlen(uartData));
        
        sprintf(uartData, "Dominant frequency: %.2f Hz\n", dominantFreq);
        bleuart.write(uartData, strlen(uartData));
        
        sprintf(uartData, "Jerking: %.2f m/s²\n", acceleration);
        bleuart.write(uartData, strlen(uartData));
        
        sprintf(uartData, "Stretch Coeff (P.D.): %.3f V\n", PotDiff);
        bleuart.write(uartData, strlen(uartData));

        // Send movement alert if needed
        if (acceleration > 2.0) {
            bleuart.write("*** Significant movement detected! ***\n", 39);
        }

        // Add a separator line
        bleuart.write("----------------------------------------\n", 41);

        char plotterData[100];
        sprintf(plotterData, "%d,%d,%d,%d\n", 
            (int)(mic),              // Sound level
            (int)(dominantFreq),     // Frequency
            (int)(acceleration*100),  // Acceleration (scaled up for visibility)
            (int)(PotDiff*100));     // Stretch (scaled up for visibility)
        bleuart.write(plotterData, strlen(plotterData));
    }

    delay(100);
}

// Put your function definitions here

// calculate RMS amplitude from samples
int32_t getPDMwave(int32_t samples) {
    long sum = 0;
    int count = 0;
    const int16_t AMPLITUDE_THRESHOLD = 10;  // Adjust this threshold based on testing to eliminate noise
    int16_t max_amplitude = 0;
    int16_t min_amplitude = 0;

    while (samples > 0) {
        if (!PDMsamplesRead) {
            yield();
            continue;
        }
        for (int i = 0; i < PDMsamplesRead; i++) {
            // Only process samples above noise threshold
            if (abs(PDMsampleBuffer[i]) > AMPLITUDE_THRESHOLD) {
                // Track min/max for peak-to-peak calculation
                if (PDMsampleBuffer[i] > max_amplitude) max_amplitude = PDMsampleBuffer[i];
                if (PDMsampleBuffer[i] < min_amplitude) min_amplitude = PDMsampleBuffer[i];
                
                // Square each sample and add to sum for RMS
                sum += (long)PDMsampleBuffer[i] * PDMsampleBuffer[i];
                count++;
            }
            samples--;
        }
        PDMsamplesRead = 0;
    }

    // Only return RMS if we have significant signal
    int32_t peak_to_peak = max_amplitude - min_amplitude;
    if (peak_to_peak > AMPLITUDE_THRESHOLD * 2) {
        return (count > 0) ? sqrt(sum / count) : 0;
    }
    return 0;  // Return 0 if signal is too weak
}

void onPDMdata() { // initialise PDM data reading
  // query the number of bytes available
  int bytesAvailable = PDM.available();

  // read into the sample buffer
  PDM.read(PDMsampleBuffer, bytesAvailable);

  // 16-bit, 2 bytes per sample
  PDMsamplesRead = bytesAvailable / 2;
}

float getBattVoltage(int x) { 
  float voltage = (x * 2 * 3.6) / 1024.0; 
  return constrain(voltage, 0.0, 4.2);  // LiPo max voltage is 4.2V
}

void VBatIndicator() { // alter neopixel colour to show battery status
  if (VBat > 4.1) {
    pixel.setPixelColor(0, pixel.Color(0, 255, 0)); // Green indicate full batt
  }
  else if (VBat < 3.4) {
    pixel.setPixelColor(0, pixel.Color(255, 0, 0)); // Red indicate low batt
  }
  else {
    pixel.setPixelColor(0, pixel.Color(0, 0, 255)); // Blue indicate otherwise
  }
  pixel.show();  // Call show() only once after setting the color
}

float computeFFT() { // compute frequency function
    // Compute FFT
    FFT.windowing(FFT_WIN_TYP_HAMMING, FFT_FORWARD);
    FFT.compute(FFT_FORWARD);
    FFT.complexToMagnitude();

    // Calculate dominant frequency
    double peak = 0;
    int peakIndex = 0;
    const double NOISE_THRESHOLD = 600;  // Adjust this value based on testing to eliminate noise
    
    for (int i = 1; i < (FFTSAMPLES/2); i++) {
        if (vReal[i] > peak) {
            peak = vReal[i];
            peakIndex = i;
        }
    }
    // Print dominant frequency
    if (peak > NOISE_THRESHOLD) {
        float dominantFreq = (peakIndex * 1.0 * FFTSAMPLING_FREQ) / FFTSAMPLES;
        return dominantFreq;
    }
    else {
        return 0.0;  // Return 0 if no significant peak found
    }

}

float getFilteredAcceleration() { // Filter out gravity from accelerometer and obtain aggregated acceleration across all 3 axes
    sensors_event_t accel;
    sensors_event_t gyro;
    sensors_event_t temp;
    lsm6ds33.getEvent(&accel, &gyro, &temp);
    
    // Low-pass filter to extract gravity components for all axes
    gravityX = ALPHA * gravityX + (1.0 - ALPHA) * accel.acceleration.x;
    gravityY = ALPHA * gravityY + (1.0 - ALPHA) * accel.acceleration.y;
    gravityZ = ALPHA * gravityZ + (1.0 - ALPHA) * accel.acceleration.z;
    
    // High-pass filter to get dynamic acceleration
    float dynamicAccelX = accel.acceleration.x - gravityX;
    float dynamicAccelY = accel.acceleration.y - gravityY;
    float dynamicAccelZ = accel.acceleration.z - gravityZ;
    
    // Calculate total magnitude of acceleration change vector
    float totalDelta = sqrt(
        pow(dynamicAccelX - lastAccelX, 2) +
        pow(dynamicAccelY - lastAccelY, 2) +
        pow(dynamicAccelZ - lastAccelZ, 2)
    );
    
    // Update last readings
    lastAccelX = dynamicAccelX;
    lastAccelY = dynamicAccelY;
    lastAccelZ = dynamicAccelZ;
    
    return totalDelta;  // Return magnitude of acceleration change
}

float getPotDiffWheat() { // calculate the potential difference across two point on wheatstone bridge
    const int SAMPLES = 10;  // Number of samples to average
    float sumA = 0;
    float sumB = 0;
    
    // Take multiple readings
    for(int i = 0; i < SAMPLES; i++) {
        sumA += analogRead(WHEATBRIDGEPIN_A);
        sumB += analogRead(WHEATBRIDGEPIN_B);
        delay(1);  // Short delay between readings
    }
    
    // Calculate average and convert to voltage
    float voltageA = (sumA / SAMPLES * 3.3) / 1024.0;
    float voltageB = (sumB / SAMPLES * 3.3) / 1024.0;
    
    return fabsf(voltageA - voltageB);
}

void setupBLE() {
    // Initialize Bluefruit with maximum connections as Peripheral
    Bluefruit.begin(1, 0);
    Bluefruit.setName("AsthmaAlly_Chest");
    
    // Configure and Start UART Service
    bleuart.begin();

    // Configure and Start Environmental Service
    envService.begin();
    
    // Configure the characteristics for ENVIRO SERVICE
    soundChar.setProperties(CHR_PROPS_READ | CHR_PROPS_NOTIFY);
    soundChar.setPermission(SECMODE_OPEN, SECMODE_NO_ACCESS);
    soundChar.setFixedLen(4);
    soundChar.begin();
    
    freqChar.setProperties(CHR_PROPS_READ | CHR_PROPS_NOTIFY);
    freqChar.setPermission(SECMODE_OPEN, SECMODE_NO_ACCESS);
    freqChar.setFixedLen(4);
    freqChar.begin();
    
    accelChar.setProperties(CHR_PROPS_READ | CHR_PROPS_NOTIFY);
    accelChar.setPermission(SECMODE_OPEN, SECMODE_NO_ACCESS);
    accelChar.setFixedLen(4);
    accelChar.begin();
    
    stretchChar.setProperties(CHR_PROPS_READ | CHR_PROPS_NOTIFY);
    stretchChar.setPermission(SECMODE_OPEN, SECMODE_NO_ACCESS);
    stretchChar.setFixedLen(4);
    stretchChar.begin();
    
    // Start advertising
    Bluefruit.Advertising.addFlags(BLE_GAP_ADV_FLAGS_LE_ONLY_GENERAL_DISC_MODE);
    Bluefruit.Advertising.addService(bleuart);     // Add UART service advertising
    Bluefruit.Advertising.addService(envService);  // ENVIRO service advertising
    Bluefruit.Advertising.addName();
    Bluefruit.Advertising.restartOnDisconnect(true);
    Bluefruit.Advertising.setInterval(32, 244);    // in unit of 0.625 ms
    Bluefruit.Advertising.setFastTimeout(30);      // number of seconds in fast mode
    Bluefruit.Advertising.start(0);                // 0 = Don't stop advertising after n seconds
}
```
### Mobile devices
- Our app takes in these data (SpO2, heart rate, sound, motion, breath) to deduce signs of imminent asthma attack
	- Wheezing (Sound Characteristics)
	- Coughing (Sound + Jerk Motion)
	- Low blood oxygen (SpO2)
	- Elevated heart rate
- The app will also analyse location data, which can eliminate false alarms
	- E.g. GPS movement indicates running -> Heart rate sensor data dropped in significance

## Circuit Schematics
![[Asthma Predictor Sensor Array.pdf]]

