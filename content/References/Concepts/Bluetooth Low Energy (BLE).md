---
tags:
  - logic
  - programming
status: Completed
---
# BLE Overview:
- Designed for low power, short-burst data transmission
- Uses GATT (Generic Attribute Profile) protocol
- Operates in 2.4GHz band
- Connection range typically 10-30m
- Not compatible with Classic Bluetooth

## Key Components:
1. GATT Hierarchy:
```
Profile
└── Service (identified by UUID)
    └── Characteristic (identified by UUID)
        └── Value (actual data)
```

2. Roles:
- Peripheral (Microcontroller): Advertises and provides data
- Central (Android phone): Scans and consumes data

## Implementation Steps:

1. Microcontroller Side:
```cpp
// Example using Arduino BLE library
#include <ArduinoBLE.h>

// Define Service UUID
BLEService myService("180D");

// Define Characteristic
BLECharacteristic myCharacteristic("2A37", 
    BLERead | BLENotify, 
    sizeof(float));

void setup() {
    BLE.begin();
    BLE.setLocalName("MyDevice");
    BLE.setAdvertisedService(myService);
    myService.addCharacteristic(myCharacteristic);
    BLE.addService(myService);
    BLE.advertise();
}

void loop() {
    // Update data
    float value = getSensorData();
    myCharacteristic.writeValue(value);
}
```

2. Android App Side:
```kotlin
// Basic structure for Android BLE implementation
class BleManager {
    private val bluetoothAdapter: BluetoothAdapter
    private val scanner: BluetoothLeScanner
    
    // Scan for devices
    private fun startScan() {
        scanner.startScan(scanCallback)
    }
    
    // Connect to device
    private fun connect(device: BluetoothDevice) {
        device.connectGatt(context, false, gattCallback)
    }
    
    // GATT callback
    private val gattCallback = object : BluetoothGattCallback() {
        override fun onCharacteristicChanged(
            gatt: BluetoothGatt,
            characteristic: BluetoothGattCharacteristic
        ) {
            // Handle received data
            val data = characteristic.value
        }
    }
}
```

## Important Considerations:

1. Permissions:
- Android requires location permission for BLE scanning
- Android 12+ requires specific Bluetooth permissions
```xml
<uses-permission android:name="android.permission.BLUETOOTH"/>
<uses-permission android:name="android.permission.BLUETOOTH_ADMIN"/>
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
```

2. Data Transfer Methods:
- Read: One-time data request
- Write: Send data to peripheral
- Notify/Indicate: Continuous updates from peripheral

3. Best Practices:
- Keep payload size small (20 bytes recommended)
- Implement reconnection logic
- Handle connection state changes
- Consider battery impact
- Implement proper error handling

4. Common Issues:
- Connection timeouts
- Device discovery problems
- Permission handling
- Android device variations
- Background operation limitations

5. Power Optimization:
- Use appropriate advertising intervals
- Minimize connection interval when possible
- Disconnect when not needed
- Use notification instead of polling

6. Security:
- Consider BLE pairing
- Implement encryption if needed
- Use bonding for trusted devices
- Validate data integrity

This overview should give you a starting point for implementing BLE communication. The exact implementation details will depend on your specific microcontroller and requirements.