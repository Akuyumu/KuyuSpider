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

## Details
### Hand mounted system
- [[I2C]] communication with [[MAX30102 - SpO2 & HeartRate]] 
- GY-MAX30102 is used for easy implementation
	- Integrated LED drivers allows a single 3.3V supply
- Investigate: Sensor on wrist or finger
- [[Adafruit Feather nRF52840 Sense]] communicates this data to user's phone via [[Bluetooth Low Energy (BLE)]]

### Chest mounted system
- Stretch of lower rib cage during breathing stretches [[Adafruit Conductive Rubber Sheet]], increasing it's resistance, creating a potential difference across a potential divider
- This P.D. is theoretically related to the stretch and thus related to the breath quantity
- This data will be calibrated to accurately represent the user's breathing via calibration in app, normalising the P.D. to the fully exhaled data and fully inhaled data
- The [[Adafruit Feather nRF52840 Sense]] reads this data and sends this data together with sound and motion data from its inbuilt sound sensor and accelerometer to the user's phone via [[Bluetooth Low Energy (BLE)]]

### Mobile devices
- Our app takes in these data (SpO2, heart rate, sound, motion, breath) to deduce signs of imminent asthma attack
	- Coughing (Sound + Jerk Motion)
	- Low blood oxygen (SpO2)
	- Elevated heart rate
- The app will also analyse location data, which can eliminate false alarms
	- E.g. GPS movement indicates running -> Heart rate sensor data dropped in significance

## Circuit Schematics
![[Asthma Predictor Sensor Array.pdf]]