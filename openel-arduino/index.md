# Getting Started with OpenEL for Arduino

[OpenEL(Open Embedded Library)](https://openel.github.io/) is a unified API(Application Programming Interface) for actuators and sensors. The specifications and implementation have been developed by [JASA(Japan Embedded Systems Technology Association)](https://www.jasa.or.jp/data/english/) since 2011.

As of November 13, 2021, version 3.2.1 is available.

## 1. Supported Hardware
- M5Stack [BALA2 ESP32 Self-balancing Robot Kit](https://shop.m5stack.com/products/bala2-esp32-self-balancing-robot-kit)

- M5Stack FIRE(in preparation)

## 2. Install Arduino IDE

1. See "Install the Arduino Desktop IDE" in the document, "[Getting Started with Arduino products](https://www.arduino.cc/en/Guide)".
2. See "Using the Library Manager" in the document, "[Installing Additional Arduino Libraries](https://www.arduino.cc/en/Guide/Libraries)" and Install [Blynk](https://blynk.io/) library.
3. See the document, "[Arduino IDE Development](https://docs.m5stack.com/en/arduino/arduino_development)" and install USB driver, M5Stack boards and M5Stack library.

## 3. Install OpenEL for Arduino

1. Download the .zip file( [openel-arduino-3.2.1.zip](https://github.com/openel/openel-arduino/releases/tag/v3.2.1) ) from the GitHub repository "[openel/openel-arduino](https://github.com/openel/openel-arduino)".
2. Open Arduino IDE.
3. See "Importing a .zip Library" in the document, "[Installing Additional Arduino Libraries](https://www.arduino.cc/en/Guide/Libraries)" and install OpenEL for Arduino.

## 4. How to use OpenEL for Arduino

1. In Arduino IDE, navigate to File > Examples > OpenEL > BALA2
2. Connect your M5Stack BALA2.
3. Verify/Compile and Upload BALA2 sketch to your M5Stack BALA2.
  - You may also need `python` (version 3) and `python-serial` module if they are not already installed to your system.
    - For Ubuntu 20.04, run the next command to install them: `sudo apt install python-is-python3 python3-serial`
4. You can see the Self-balancing Robot running slowly.

### 4.1 How to connect to BALA2 by using Blynk

1. Sign Up [Blynk](https://blynk.cloud/dashboard/register) and get your "Blynk Auth Token".
2. Write your token into the following line in [BALA2.ino](https://github.com/openel/openel-arduino/blob/v3.2.0/examples/BALA2/BALA2.ino).
```
47 : #define AUTH "My Blynk Auth Token" // Your Blynk Auth Token
```
3. Verify/Compile and Upload BALA2 sketch to your M5Stack BALA2.
4. See the document, "[Build your first IoT app in five minutes](https://blynk.io/en/getting-started)" and download and install [Blynk(legacy)](https://play.google.com/store/apps/details?id=cc.blynk) application to youe Android or iPhone..

5. Set up Joystick Settinngs in your Blynk(legacy) application.
```
OUTPUT
mode:MERGE
name:V0
[0]:from -1 to +1
[1]:from -1 to +1
AUTORETURN:ON
ROTATE ON TILT:ON
WRITE INTERVAL:100ms
```
6. Connect to BALA2.
7. Enjoy!

## 5. How to add a new device

1. Apply to JASA for Device Kind ID(Only if you want to add a new kind of device) and Vendor ID assignment.
2. Change to the OpenEL source directory, Arduino/libraries/openel-arduino-3.2.0/src
3. Copy and Rename HAL Component file( openEL_Actuatorxxx.hpp and openEL_Actuatorxxx.cpp or openEL_Sensorxxx.hpp and openEL_Sensorxxx.cpp).
4. File name naming convention is the following. DeviceName is required if the product has multiple devices of the same type.

```
openEL_[Device Kind][ProductName][DeviceName]

ex.
openEL_SensorM5StackGrayBMM150.cpp
openEL_SensorM5StackGrayBMM150.hpp
openEL_SensorM5StackGrayMPU6886.cpp
openEL_SensorM5StackGrayMPU6886.hpp
```

5. Edit your HAL Component file.
6. Add your header file and Hal Registration Table into openEL_registoryConfig.cpp file.
7. You can use your new device from your sketch by using deviceKindId, vendorId, productId, and instanceId.

```
ex.
  Actuator *motor_l = 0;
  Actuator *motor_r = 0;
  Sensor *IMU = 0;
  Sensor *BMM = 0;

  HALId halid1, halid2, halid3, halid4;
  halid1.deviceKindId = 0x1;  // Motor
  halid1.vendorId = 0xA;      // M5Stack
  halid1.productId = 0x1;     // BALA2
  halid1.instanceId = 0x1;    // Left Motor

  halid2.deviceKindId = 0x1;
  halid2.vendorId = 0xA;
  halid2.productId = 0x1;
  halid2.instanceId = 0x2;    // Right Motor

  halid3.deviceKindId = 0x2;  // Gyroscope Sensor
  halid3.vendorId = 0xA;
  halid3.productId = 0x1;
  halid3.instanceId = 0x1;

  halid4.deviceKindId = 0xD;  // Magnetic Sensor
  halid4.vendorId = 0xA;
  halid4.productId = 0x1;
  halid4.instanceId = 0x1;

  motor_l = new Actuator(halid1);
  motor_r = new Actuator(halid2);
  IMU = new Sensor(halid3);
  BMM = new Sensor(halid4);
```

## 6. How to Add your HAL Component file to repository
1. Fork openel-arduino repository.
2. Add and Commit your HAL Compornent file to your repository.
3. Create a pull request.

We look forward to your pull request.
