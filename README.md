# Lab 1: Introduction to Mbed

## Learning Outcome
Understand the architecture of an embedded system and how to build and run a program using Mbed OS.

## Introduction
This lab introduces the **ST DISCO L475VG** development board and the Arm Mbed development ecosystem, familiarizing you with the development process for future labs.

## Resources

### Hardware
This lab uses the **ST DISCO L475VG** development board, referred to as "the board" in this and future labs.

#### Board Specification
- **Storage:**
  - 64-Mbit Quad-SPI (Macronix) Flash memory
- **Connectivity:**
  - Bluetooth® V4.1 module (SPBTLE-RF)
  - Sub-GHz (868 or 915MHz) low-power-programmable RF module (SPSGRF-868 or SPSGRF-915)
  - Wi-Fi® module Inventek ISM43362-M3G-L44 (802.11 b/g/n compliant)
  - Dynamic Near-field Communication (NFC) tag based on M24SR with printed NFC antenna
- **Input/Output (IO):**
  - Two digital omnidirectional microphones (MP34DT01)
  - Capacitive digital sensor for relative humidity and temperature (HTS221)
  - High-performance 3-axis magnetometer (LIS3MDL)
  - 3D accelerometer and 3D gyroscope (LSM6DSL)
  - 260-1260hPa absolute digital output barometer (LPS22HB)
  - Time-of-Flight and gesture-detection sensor (VL53L0X)
  - Two push-buttons (user and reset)
- **Communication:**
  - USB OTG FS with Micro-AB connector
- **Expansion connectors:**
  - Arduino™ Uno V3
  - PMOD
- Flexible power-supply options: ST LINK USB VBUS or external sources
- On-board ST-LINK/V2-1 debugger/programmer with USB re-enumeration capability: mass storage, virtual COM port, and debug port

#### Board Pinout
A *pinout* describes the function of each physical connection (pin) on the board. The pin diagrams include:

- **Arduino Compatible Headers**:
  - Left-hand Side
  - Right-hand Side

Some pins have multiple functions, configurable in software (e.g., SPI, I2C). For example, to use SPI2, pins PD_1, PD_3, PD_4, and PD_0 must be reconfigured from GPIOs to SPI2_SCLK, SPI2_MISO, SPI2_MOSI, and SPI2_SSEL.

### Software
You need a computer, an internet connection, and the Mbed Studio IDE. You can also set up a local development environment.

### Communicating with the Board
The board appears as a removable disk drive (like a USB stick) when connected via USB, called *mounting*. To program the board, copy the compiled program (.bin file) to the virtual disk drive (named “DAPLINK” or the board’s name).

**Try this now:** Connect the board to your computer using a USB cable and observe the drive appear.

**Notes for Operating Systems:**
- **Windows:** The virtual drive appears in “Computer.”
- **Mac:** The virtual drive appears on the desktop.
- **Linux:** The virtual drive may auto-mount, or you can manually mount it using the `mount` command after checking `dmesg` output for the latest USB storage device.

## Mbed Studio Setup
Mbed Studio is a free IDE for creating Mbed OS 6 applications and libraries. Download and install it from: [https://os.mbed.com/studio/](https://os.mbed.com/studio/). Register for an account and sign in when launching the IDE.

### Preparing a Workspace
Upon installation, Mbed Studio creates a workspace named “Mbed Programs” in your home directory to store your Mbed programs, including imported and created projects. To change the workspace:
1. Click **File** > **Open Workspace**.
2. Navigate to and select the desired folder.

### Creating or Importing Programs
To create a new program:
1. Open **File** > **New Program**.
2. Select “Empty Mbed OS program” to start from scratch or choose a pre-written example.
3. Name the program in the “Program Name” field and click **Add Program** (ensure “make this the active program” is ticked).

To import the “mbed-os-example-blinky” project:
1. Open **File** > **New Program**.
2. Select “mbed-os-example-blinky” from the dropdown and click **Add Program**.

The program will appear in the explorer on the left-hand side of the IDE.

### Building and Running a Program
1. Connect your Mbed-enabled board and select it from the target list in Mbed Studio.
2. Ensure “mbed-os-example-blinky” is the active program, then click **Build program**.
3. Mbed Studio creates a .bin file (compiled machine code). Copy this file to the board’s internal storage to load and run the program (e.g., blinking LED).
4. Alternatively, click **Run program** to automatically build and copy the program to the board.

## Exercise
Write an embedded application that executes a continuous loop where:
- LED 1 and LED 2 on the board blink once every second consecutively.
- Both LEDs flash simultaneously for a second.
- The process repeats.

# Lab 2: Sensors

## Learning Outcome
Understand how to access on-board sensors and use serial communication to transfer data.

## Introduction
### Lab Overview
This lab teaches you to interface with environmental sensors on the DISCO-L475VG-IOT01A board using the Mbed API. The board includes:
- Pressure sensor (LPS22HB)
- 3-axis accelerometer and gyroscope (LSM6DSL)
- 3-axis magnetometer (LIS3MDL)
- Humidity and temperature sensor (HTS221)
- Time-of-Flight and gesture-detection sensor (VL53L0X)
- Two digital omnidirectional microphones (MP34DT01)

You will read sensor data, transmit it to a PC via UART, and display the readings on a terminal emulator.

## Requirements

### Software Functions
#### UART Functions
Use the `BufferedSerial` API to communicate with the PC.

#### On-board Sensor Functions
**Initialization of Sensors:**
- `HTS221TemperatureBSP_TSENSOR_Init()`
- `HumidityBSP_HSENSOR_Init()`
- `LPS22HBPressureBSP_PSENSOR_Init()`
- `LIS3MDLMagnetometerBSP_MAGNETO_Init()`
- `LSM6DSLAccelerometerBSP_ACCELERO_Init()`
- `GyroscopeBSP_GYRO_Init()`

**Reading Data from Sensors:**
- `float BSP_TSENSOR_ReadTemp(void)`: Temperature reading from HTS221.
- `float BSP_HSENSOR_ReadHumidity(void)`: Humidity reading from HTS221.
- `float BSP_PSENSOR_ReadPressure(void)`: Pressure reading from LPS22HB.
- `void BSP_MAGNETO_GetXYZ(int16_t *pDataXYZ)`: 3-axis magnetometer values.
- `void BSP_MAGNETO_LowPower(uint16_t status)`: Activates magnetometer low power mode.
- `void BSP_GYRO_GetXYZ(float* pfData)`: 3-axis gyroscope values.
- `void BSP_GYRO_LowPower(uint16_t status)`: Activates gyroscope low power mode.
- `void BSP_ACCELERO_AccGetXYZ(int16_t *pDataXYZ)`: 3-axis accelerometer values.
- `void BSP_ACCELERO_LowPower(uint16_t status)`: Activates accelerometer low power mode.

## Getting Set-up
Include the board support files for the DISCO-L475VG-IOT01A from: [https://os.mbed.com/teams/ST/code/BSP_B-L475E-IOT01/](https://os.mbed.com/teams/ST/code/BSP_B-L475E-IOT01/). In Mbed Studio, go to **File** > **Add Library to Active Program**, paste the URL, and select the default/master branch.

Enable floating-point support in `mbed_lib.json` by setting:
- `minimal-printf-enable-64-bit`
- `minimal-printf-enable-floating-point`

## Application Code
Write a program to:
- Read temperature, humidity, pressure, magnetometer, accelerometer, and gyroscope values every three seconds.
- Convert temperature to Fahrenheit and Kelvin.
- Enter sleep mode and wait for interrupts.
- Blink an LED every second to indicate responsiveness.
- Display sensor readings via the serial debug interface.

### Program Structure
- **Global Variables:**
  - `BufferedSerial` object for PC communication.
  - `DigitalOut` object for the LED.
  - Two `LowPowerTicker` objects:
    - One for flashing the LED every second.
    - One for triggering sensor readings.
- **Initialization:**
  - Initialize sensors.
  - Print a welcome message.
  - Activate tickers.
- **Ticker Handlers:**
  - Toggle the LED and update measurements.
  - Set a flag to indicate when measurements should be read and displayed.
- **Main Function:**
  - In a loop:
    - Check if the flag is set.
    - Read from sensors.
    - Convert temperature to Fahrenheit and Kelvin.
    - Write output to UART.
    - Enter sleep mode.

### Global Variables
```cpp
static DigitalOut led(LED1);
static BufferedSerial serial_port(USBTX, USBRX, 9600);

FileHandle *mbed::mbed_override_console(int fd)
{
    return &serial_port;
}
```

### Initialization
```cpp
int main()
{
    led = true;
    printf("Hello, world.\n");
    return 0;
}
```

### Tickers
**Global Variables:**
```cpp
static LowPowerTicker ledTicker;
static LowPowerTicker readoutTicker;
static bool shouldReadSensors;
```

**Handlers:**
```cpp
static void ledTick()
{
    led = !led;
}

static void readoutTick()
{
    shouldReadSensors = true;
}
```

**Initialization Code:**
```cpp
ledTicker.attach(&ledTick, 1s);
readoutTicker.attach(&readoutTick, 3s);
```

Compile and run the program to verify the LED toggles every second.

### Reading from Sensors
Initialize sensors:
```cpp
static void initialiseSensors()
{
    BSP_TSENSOR_Init();
    BSP_HSENSOR_Init();
    BSP_PSENSOR_Init();
    BSP_MAGNETO_Init();
    BSP_ACCELERO_Init();
    BSP_GYRO_Init();
}
```

Call from main:
```cpp
int main()
{
    ...
    initialiseSensors();
    ...
}
```

Read and display sensor values:
```cpp
static void readSensors()
{
    printf("Sensor values:\n");
    float temp = BSP_TSENSOR_ReadTemp();
    printf("* Temperature: %f C, %f F, %f K\n",
           temp,
           convertCelsiusToFahrenheit(temp),
           convertCelsiusToKelvin(temp));
    ...
}
```

Implement `convertCelsiusToFahrenheit` and `convertCelsiusToKelvin` functions and display data from other sensors.

In the main loop:
```cpp
while (true) {
    sleep();
    if (shouldReadSensors) {
        readSensors();
        shouldReadSensors = false;
    }
}
```

### Expected Output
```
Hello, world.
Sensor values:
* Temperature: 24.369190 C, 75.864540 F, 297.519196 K
* Humidity: 53.434387
* Pressure: 1000.169983
* Magneto: 80 -433 221
* Gyro: 0.000000 -1120.000000 770.000000
* Accelerometer: 5 -1 1011
```

(Your sensor values will vary.)

# Lab 3: Local Connectivity

## Learning Outcome
Understand how Bluetooth Low Energy (BLE) communication works and how to transmit and receive basic data.

## Introduction
### Lab Overview
Learn to communicate with the outside world via BLE, programming the embedded device to transmit live sensor data to a mobile app that supports BLE.

## Hardware and Software Requirements
- DISCO-L475VG-IOT01A board
- Android mobile phone with a Bluetooth LE Scanner App
- Mbed Studio or another suitable development environment
- Include the BLE utility library: [https://github.com/ARMmbed/mbed-os-ble-utils](https://github.com/ARMmbed/mbed-os-ble-utils)
- Include the board support library as in Lab 2.

## Working with Bluetooth
Refer to:
- Mbed OS Bluetooth APIs: [https://os.mbed.com/docs/mbed-os/v6.10/apis/bluetooth-apis.html](https://os.mbed.com/docs/mbed-os/v6.10/apis/bluetooth-apis.html)
- BLE examples: [https://github.com/ARMmbed/mbed-os-example-ble/](https://github.com/ARMmbed/mbed-os-example-ble/)

## Configuration
BLE can be complex, but efficient coding simplifies the process.

## Application Code
Program the device to:
- Advertise its presence over BLE.
- Transmit live temperature, humidity, and pressure sensor readings.
- Allow remote toggling of the on-board LED.

### High-Level Overview
- Initialize BLE.
- Advertise presence.
- Accept connections and periodically transmit sensor readings.
- Respond to write events to toggle the LED.

### Initializing BLE
Create a class to manage the BLE process:
```cpp
class Lab3ServerProcess : public BLEProcess {
public:
    Lab3ServerProcess(events::EventQueue &event_queue, BLE &ble_interface)
        : BLEProcess(event_queue, ble_interface) {}
    const char *get_device_name() override {
        static const char name[] = "Lab 3 Server";
        return name;
    }
};
```

Create a server class to manage the service and characteristics:
```cpp
class Lab3Server : ble::GattServer::EventHandler {
public:
    Lab3Server() {}
    ~Lab3Server() {}
    void start(BLE &ble, events::EventQueue &event_queue) {
        const UUID uuid = GattService::UUID_ENVIRONMENTAL_SERVICE;
        GattCharacteristic *charTable[] = {};
        GattService sensorService(uuid, charTable,
                                 sizeof(charTable) / sizeof(charTable[0]));
        ble.gattServer().addService(sensorService);
        ble.gattServer().setEventHandler(this);
        printf("Service started.\n");
    }
};
```

Initialize BLE in main:
```cpp
static EventQueue event_queue(10 * EVENTS_EVENT_SIZE);
int main() {
    BLE &ble = BLE::Instance();
    printf("Lab 3 - BLE");
    Lab3ServerProcess ble_process(event_queue, ble);
    Lab3Server server;
    ble_process.on_init(callback(&server, &Lab3Server::start));
    ble_process.start();
    return 0;
}
```

Build and run, then use a BLE scanning app to verify the “Environmental” service appears.

### Advertising Sensor Data
Initialize sensors:
```cpp
static void initialiseSensors() {
    BSP_TSENSOR_Init();
    BSP_HSENSOR_Init();
    BSP_PSENSOR_Init();
}
```

Create a helper class for sensor characteristics:
```cpp
class SensorReadingCharacteristic : public GattCharacteristic {
public:
    SensorReadingCharacteristic(const UUID &uuid)
        : GattCharacteristic(
              uuid, (uint8_t *)&stringRepr_, sizeof(stringRepr_),
              sizeof(stringRepr_),
              GattCharacteristic::BLE_GATT_CHAR_PROPERTIES_READ |
                  GattCharacteristic::BLE_GATT_CHAR_PROPERTIES_NOTIFY),
          internalValue_(0) {
        updateStringRepr();
    }
    void updateValue(BLE &ble, float newValue) {
        internalValue_ = newValue;
        updateStringRepr();
        ble.gattServer().write(getValueHandle(), (uint8_t *)&stringRepr_,
                               sizeof(stringRepr_));
    }
private:
    float internalValue_;
    uint8_t stringRepr_[16];
    void updateStringRepr() {
        sprintf((char *)stringRepr_, "%f", internalValue_);
    }
};
```

Add sensor characteristics to `Lab3Server`:
```cpp
class Lab3Server : ble::GattServer::EventHandler {
public:
    Lab3Server()
        : temperature_(GattCharacteristic::UUID_TEMPERATURE_CHAR),
          humidity_(GattCharacteristic::UUID_HUMIDITY_CHAR),
          pressure_(GattCharacteristic::UUID_PRESSURE_CHAR) {}
private:
    SensorReadingCharacteristic temperature_;
    SensorReadingCharacteristic humidity_;
    SensorReadingCharacteristic pressure_;
};
```

Update the characteristics array in the `start` method:
```cpp
GattCharacteristic *charTable[] = {&temperature_, &humidity_, &pressure_};
```

Update sensor values every second:
```cpp
void updateSensors(BLE &ble) {
    printf("Updating sensors...\n");
    temperature_.updateValue(ble, BSP_TSENSOR_ReadTemp());
    humidity_.updateValue(ble, BSP_HSENSOR_ReadHumidity());
    pressure_.updateValue(ble, BSP_PSENSOR_ReadPressure());
}
```

Schedule updates:
```cpp
event_queue.call_every(1000ms, [this, &ble] { updateSensors(ble); });
```

Verify sensor data appears in the BLE scanner app.

### Toggling the LED
Add fields to `Lab3Server`:
```cpp
DigitalOut led_;
uint8_t ledValue_;
ReadWriteGattCharacteristic<uint8_t> ledChar_;
```

Update the constructor:
```cpp
Lab3Server()
    : temperature_(GattCharacteristic::UUID_TEMPERATURE_CHAR),
      humidity_(GattCharacteristic::UUID_HUMIDITY_CHAR),
      pressure_(GattCharacteristic::UUID_PRESSURE_CHAR),
      led_(LED1),
      ledValue_(0),
      ledChar_(0xA000, &ledValue_) {}
```

Add the LED characteristic to the char table:
```cpp
GattCharacteristic *charTable[] = {&temperature_, &humidity_, &pressure_, &ledChar_};
```

Implement the LED control method:
```cpp
virtual void onDataWritten(const GattWriteCallbackParams &params) override {
    if ((params.handle == ledChar_.getValueHandle()) && (params.len == 1)) {
        printf("New LED value: %x\r\n", *(params.data));
        ledValue_ = *(params.data);
        led_ = ledValue_;
    }
}
```

Build and run to verify LED toggling via the BLE scanner app (write 1 to turn on, 0 to turn off).

# Lab 4: Global Connectivity

## Learning Outcome
Understand how wireless technology connects to a cloud-based IoT service and how a full-stack implementation works.

## Introduction
### Lab Overview
Program the embedded device to transmit sensor data via Wi-Fi to a serverless function in Google Cloud, which decodes and stores the data in a database. Build a simple website to display the data.

## Hardware and Software Requirements
- DISCO-L475VG-IOT01A board
- Mbed Studio or another suitable development environment
- Google Cloud account: [https://cloud.google.com](https://cloud.google.com) (additional charges may apply if usage limits are exceeded)

## Getting Started
### The Development Board
Create a blank Mbed OS 6 project and add:
- Board Support files: [https://os.mbed.com/teams/ST/code/BSP_B-L475E-IOT01/](https://os.mbed.com/teams/ST/code/BSP_B-L475E-IOT01/)
- ISM43362 Wi-Fi component: [https://github.com/ARMmbed/wifi-ism43362/](https://github.com/ARMmbed/wifi-ism43362/)
- Mbed OS 6 HTTP client: [https://github.com/rasmus0201/mbed-http-client.git](https://github.com/rasmus0201/mbed-http-client.git)

Create an `mbed_app.json` file with:
```json
{
    "target_overrides": {
        "*": {
            "nsapi.default-wifi-security": "WPA_WPA2",
            "nsapi.default-wifi-ssid": "\"<YOUR-SSID>\"",
            "nsapi.default-wifi-password": "\"<YOUR-PASSWORD>\"",
            "platform.stdio-baud-rate": 115200,
            "rtos.main-thread-stack-size": 8192,
            "target.printf_lib": "std"
        },
        "DISCO_L475VG_IOT01A": {
            "target.components_add": ["ism43362"],
            "ism43362.provide-default": true,
            "target.network-default-interface-type": "WIFI"
        }
    }
}
```
Replace `<YOUR-SSID>` and `<YOUR-PASSWORD>` with your Wi-Fi credentials.

### The Cloud
Create a Google Cloud project (e.g., “arm-edx-lab4”) in the Google Cloud Console: [https://console.cloud.google.com](https://console.cloud.google.com). Note the **Project ID**.

Enable and pin the “Cloud Functions” and “Firestore” services. Set up Firestore in **Native Mode** and select a nearby location.

Create a service account:
1. Navigate to **Credentials** > **Manage service accounts** > **Create service account**.
2. Name it (e.g., “datastore”) and assign the “Cloud Datastore User” role.
3. Create a JSON key and save it securely.

## Cloud Functions
### The “StoreSensorData” Function
Create a Cloud Function named “StoreSensorData” with an HTTP trigger, allowing unauthenticated invocations and disabling HTTPS. Set the entry point to “storeData” and add to `index.js` (replace `<YOUR-PROJECT-ID>`):
```javascript
const Firestore = require('@google-cloud/firestore');
const db = new Firestore({
    projectId: '<YOUR-PROJECT-ID>',
    keyFilename: 'key.json'
});
exports.storeData = async (req, res) => {
    const messageData = req.body;
    if (messageData === undefined || messageData === null) {
        console.error('Unable to read message');
        res.status(400).send();
        return;
    }
    const timestamp = Date.now();
    await db.collection('sensor-data').add({
        timestamp,
        ...messageData
    });
    res.status(200).send();
};
```

Update `package.json`:
```json
{
    "name": "store-sensor-data",
    "version": "0.0.1",
    "dependencies": {
        "@google-cloud/firestore": "^6.4.2"
    }
}
```

Add the service account key to `key.json`. Deploy the function and grant “Cloud Functions Invoker” role to “allUsers”. Test with:
```json
{
    "temperature": 20.5,
    "humidity": 66.1234,
    "pressure": 999.45
}
```

Verify data in Firestore.

### The “GetRecentSensorData” Function
Create a Cloud Function named “GetRecentSensorData” with an HTTP trigger, allowing unauthenticated invocations. Set the entry point to “getData” and add to `index.js` (replace `<YOUR-PROJECT-ID>`):
```javascript
const Firestore = require('@google-cloud/firestore');
const db = new Firestore({
    projectId: '<YOUR-PROJECT-ID>',
    keyFilename: 'key.json'
});
exports.getData = async (req, res) => {
    res.set('Access-Control-Allow-Origin', '*');
    if (req.method === 'OPTIONS') {
        res.set('Access-Control-Allow-Methods', 'GET');
        res.set('Access-Control-Allow-Headers', 'Content-Type');
        res.set('Access-Control-Max-Age', '3600');
        res.status(204).send('');
    } else {
        const coll = db.collection('sensor-data');
        const sensorDataSnapshot = await coll
            .orderBy('timestamp')
            .limit(10)
            .get();
        const sensorData = sensorDataSnapshot.docs.map(doc => doc.data());
        res.json(sensorData);
    }
};
```

Update `package.json` as above and add the service account key to `key.json`. Deploy and grant “Cloud Functions Invoker” role to “allUsers”. Test to verify data retrieval.

## Sending Sensor Readings
Include necessary headers:
```cpp
#include "http_request.h"
#include "mbed.h"
#include "stm32l475e_iot01.h"
#include "stm32l475e_iot01_hsensor.h"
#include "stm32l475e_iot01_psensor.h"
#include "stm32l475e_iot01_tsensor.h"
static BufferedSerial serial_port(USBTX, USBRX, 9600);
FileHandle *mbed::mbed_override_console(int fd)
{
    return &serial_port;
}
```

Initialize sensors:
```cpp
static void initialiseSensors() {
    BSP_TSENSOR_Init();
    BSP_HSENSOR_Init();
    BSP_PSENSOR_Init();
}
```

Send sensor data (replace `<YOUR-TRIGGER-URL>` with the HTTP trigger URL for “StoreSensorData”):
```cpp
static void sendSensorData(NetworkInterface *net) {
    const char messageFormat[] =
        "{ \"temperature\": %f, \"humidity\": %f, \"pressure\": %f }";
    char messageData[256] = {0};
    sprintf(messageData, messageFormat, BSP_TSENSOR_ReadTemp(),
            BSP_HSENSOR_ReadHumidity(), BSP_PSENSOR_ReadPressure());
    auto *req = new HttpRequest(
        net, HTTP_POST,
        "http://<YOUR-TRIGGER-URL>");
    req->set_header("Content-Type", "application/json");
    printf("Sending message: %s\n", messageData);
    HttpResponse *res = req->send(messageData, strlen(messageData));
    if (!res) {
        printf("Http request failed (error code %d)\n", req->get_error());
    }
    delete req;
}
```

Main function:
```cpp
int main() {
    printf("Initialising sensors...\n");
    initialiseSensors();
    auto net = NetworkInterface::get_default_instance();
    printf("Connecting to the network...\r\n");
    nsapi_size_or_error_t result = net->connect();
    if (result != 0) {
        printf("Error! net->connect() returned: %d\r\n", result);
        return -1;
    }
    SocketAddress ipaddr;
    net->get_ip_address(&ipaddr);
    printf("Connected with IP address: %s\r\n",
           ipaddr.get_ip_address() ? ipaddr.get_ip_address() : "(none)");
    while (true) {
        sendSensorData(net);
        ThisThread::sleep_for(1s);
    }
}
```

Build and run to verify data appears in Firestore. Avoid prolonged connections to prevent exceeding free usage limits.

## The Web Application
Create `view.html` to display sensor data:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Sensor Data Viewer</title>
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
</head>
<body>
    <h1>Sensor Data</h1>
    <table id="data-table" border="1">
        <thead>
            <tr>
                <th>Time</th>
                <th>Temperature</th>
                <th>Humidity</th>
                <th>Pressure</th>
            </tr>
        </thead>
        <tbody></tbody>
    </table>
    <script>
        const dataTable = document.getElementById('data-table');
        const dataTableBody = dataTable.getElementsByTagName('tbody')[0];
        function loadData() {
            dataTableBody.innerHTML = '';
            axios.get('URL-TO-YOUR-CLOUD-FUNCTION').then(function (data) {
                for (const reading of data.data) {
                    const row = document.createElement('tr');
                    const timeCell = document.createElement('td');
                    const ts = new Date(reading.timestamp);
                    timeCell.innerText = ts.toLocaleString('en-GB');
                    row.appendChild(timeCell);
                    const tempCell = document.createElement('td');
                    tempCell.innerHTML = reading.temperature.toFixed(1) + ' &deg;C';
                    row.appendChild(tempCell);
                    const humCell = document.createElement('td');
                    humCell.innerText = reading.humidity.toFixed(0) + '%';
                    row.appendChild(humCell);
                    const presCell = document.createElement('td');
                    presCell.innerText = reading.pressure.toFixed(1);
                    row.appendChild(presCell);
                    dataTableBody.appendChild(row);
                }
            });
        }
        setInterval(loadData, 5000);
        loadData();
    </script>
</body>
</html>
```

Replace `URL-TO-YOUR-CLOUD-FUNCTION` with the “GetRecentSensorData” trigger URL. Upload `view.html` to a Google Cloud Storage bucket (e.g., “lab4-sensor-data-viewer”). Access the “Authenticated URL” to view the web page.

# Lab 5: The Cloud

## Learning Outcome
Understand how to develop a full-stack IoT system.

## Introduction
Combine experiences from previous labs to create a system that:
- Collects accelerometer and gyroscope data.
- Sends batches of data to a cloud service for activity classification.
- Displays activity periods in an Android app.

## The “ProcessSensorData” Function
Create a Cloud Function named “ProcessSensorData” with an HTTP trigger, allowing unauthenticated invocations. Set the entry point to “processData” and add to `index.js` (replace `YOUR-PROJECT-ID`):
```javascript
const Firestore = require('@google-cloud/firestore');
const db = new Firestore({
    projectId: 'YOUR-PROJECT-ID',
    keyFilename: 'key.json'
});
function computeMean(array) {
    return array.reduce((a, b) => a + b) / array.length;
}
function computeStdDev(array) {
    const mean = computeMean(array);
    return Math.sqrt(array.reduce((a, b) => a + Math.pow(b - mean, 2), 0) / array.length);
}
function predict(inputData) {
    return { label: 'still' };
}
exports.processData = async (req, res) => {
    const messageData = req.body;
    if (messageData === undefined || messageData.readings === undefined) {
        console.error('Unable to read message');
        res.status(400).send();
        return;
    }
    const accelX = [], accelY = [], accelZ = [];
    const gyroX = [], gyroY = [], gyroZ = [];
    for (const reading of messageData.readings) {
        accelX.push(reading.accel.x);
        accelY.push(reading.accel.y);
        accelZ.push(reading.accel.z);
        gyroX.push(reading.gyro.x);
        gyroY.push(reading.gyro.y);
        gyroZ.push(reading.gyro.z);
    }
    const inputData = {
        acceleration_x_mean: computeMean(accelX).toFixed(6),
        acceleration_x_std: computeStdDev(accelX).toFixed(6),
        acceleration_y_mean: computeMean(accelY).toFixed(6),
        acceleration_y_std: computeStdDev(accelY).toFixed(6),
        acceleration_z_mean: computeMean(accelZ).toFixed(6),
        acceleration_z_std: computeStdDev(accelZ).toFixed(6),
        gyro_x_mean: computeMean(gyroX).toFixed(6),
        gyro_x_std: computeStdDev(gyroX).toFixed(6),
        gyro_y_mean: computeMean(gyroY).toFixed(6),
        gyro_y_std: computeStdDev(gyroY).toFixed(6),
        gyro_z_mean: computeMean(gyroZ).toFixed(6),
        gyro_z_std: computeStdDev(gyroZ).toFixed(6)
    };
    const prediction = predict(inputData);
    console.log('Activity data processed: ', prediction);
    const timestamp = Date.now();
    await db.collection('activity-data').add({
        timestamp,
        activity: prediction.label
    });
    res.status(200).send();
};
```

Update `package.json`:
```json
{
    "name": "process-sensor-data",
    "version": "0.0.1",
    "dependencies": {
        "@google-cloud/firestore": "^6.4.2"
    }
}
```

Add the service account key to `key.json`. Deploy and grant “Cloud Functions Invoker” role to “allUsers”. Test with:
```json
{
    "readings": [
        {
            "accel": {
                "x": 1,
                "y": 1,
                "z": 1
            },
            "gyro": {
                "x": 1,
                "y": 1,
                "z": 1
            }
        }
    ]
}
```

Verify the classification in Firestore.

## The “GetActivityData” Function
Create a Cloud Function named “GetActivityData” with an HTTP trigger, allowing unauthenticated invocations. Set the entry point to “getData” and add to `index.js` (replace `YOUR-PROJECT-ID`):
```javascript
const Firestore = require('@google-cloud/firestore');
const db = new Firestore({
    projectId: 'YOUR-PROJECT-ID',
    keyFilename: 'key.json'
});
exports.getData = async (req, res) => {
    res.set('Access-Control-Allow-Origin', '*');
    if (req.method === 'OPTIONS') {
        res.set('Access-Control-Allow-Methods', 'GET');
        res.set('Access-Control-Allow-Headers', 'Content-Type');
        res.set('Access-Control-Max-Age', '3600');
        res.status(204).send('');
    } else {
        const coll = db.collection('activity-data');
        const activityDataSnapshot = await coll.orderBy('timestamp').get();
        const activityData = activityDataSnapshot.docs.map(doc => doc.data());
        res.json(activityData);
    }
};
```

Update `package.json` as above and add the service account key to `key.json`. Deploy and grant “Cloud Functions Invoker” role to “allUsers”. Test to verify data retrieval.

## Sending Gyro and Accelerometer Data
Copy the Lab 4 project, naming it “Lab 5”. Update `mbed_app.json` and add libraries as in Lab 4. Initialize accelerometer and gyroscope:
```cpp
static void initialiseSensors() {
    BSP_ACCELERO_Init();
    BSP_GYRO_Init();
}
```

Add helper routines:
```cpp
struct SensorData {
    int16_t accel[3];
    float gyro[3];
};
static std::vector<SensorData> batchedSensorData;
static SensorData readSensors() {
    printf("Reading sensors...\n");
    SensorData d;
    BSP_ACCELERO_AccGetXYZ(d.accel);
    BSP_GYRO_GetXYZ(d.gyro);
    return d;
}
static void sendReadings(NetworkInterface *net) {
    std::string messageData = "{ \"readings\": [";
    bool first = true;
    for (const auto &sd : batchedSensorData) {
        if (first) {
            first = false;
        } else {
            messageData += ", ";
        }
        messageData += "{ \"accel\": { ";
        messageData += "\"x\": " + std::to_string(sd.accel[0]) + ", ";
        messageData += "\"y\": " + std::to_string(sd.accel[1]) + ", ";
        messageData += "\"z\": " + std::to_string(sd.accel[2]) + " }, ";
        messageData += "\"gyro\": { ";
        messageData += "\"x\": " + std::to_string(sd.gyro[0]) + ", ";
        messageData += "\"y\": " + std::to_string(sd.gyro[1]) + ", ";
        messageData += "\"z\": " + std::to_string(sd.gyro[2]) + " } }";
    }
    messageData += "] }";
    auto *req = new HttpRequest(
        net, HTTP_POST,
        "<YOUR-TRIGGER-URL>");
    req->set_header("Content-Type", "application/json");
    printf("Sending message: %s\n", messageData.c_str());
    HttpResponse *res = req->send(messageData.c_str(), messageData.length());
    if (!res) {
        printf("Http request failed (error code %d)\n", req->get_error());
    }
    delete req;
}
```

Replace `<YOUR-TRIGGER-URL>` with the “ProcessSensorData” trigger URL. Update `sendSensorData`:
```cpp
static void sendSensorData(NetworkInterface *net) {
    auto sensorData = readSensors();
    batchedSensorData.push_back(sensorData);
    if (batchedSensorData.size() >= 5) {
        sendReadings(net);
        batchedSensorData.clear();
    }
}
```

Use the same main function as Lab 4. Build and run to verify data in Firestore.

## Viewing Activity History
### Building the App
#### Getting Started
Use an Android phone in developer mode and install Android Studio: [https://developer.android.com/studio](https://developer.android.com/studio). Create a new project with an “Empty Views Activity” using Java.

#### Overview
The app includes a switch to interrogate the “GetActivityData” function every five seconds and display activity periods in a table.

#### Designing the User Interface
Open `activity_main.xml` in Android Studio. Delete the “Hello World!” text and add:
- **ProgressBar** (ID: `loadingProgress`)
- **ScrollView** containing a **TableLayout** (ID: `resultsTable`)
- **Switch** (ID: `activateLoaderSwitch`, text: “Activate Loader”)

Position components using ConstraintLayout:
- Constrain the switch’s bottom to the parent.
- Constrain the ScrollView’s bottom to the switch’s top and top to the ProgressBar’s bottom.

Test the app to verify the UI.

#### Reading and Processing Activity Data
Edit `MainActivity.java`:
```java
package com.example.lab5activitytracker;
import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.os.Handler;
import android.os.Message;
import android.view.View;
import android.widget.CompoundButton;
import android.widget.Space;
import android.widget.Switch;
import android.widget.TableLayout;
import android.widget.TableRow;
import android.widget.TextView;
import com.android.volley.Request;
import com.android.volley.RequestQueue;
import com.android.volley.Response;
import com.android.volley.VolleyError;
import com.android.volley.toolbox.StringRequest;
import com.android.volley.toolbox.Volley;
import org.json.JSONArray;
import org.json.JSONException;
import org.json.JSONObject;
import java.text.DateFormat;
import java.util.Date;
import java.util.Timer;
import java.util.TimerTask;
public class MainActivity extends AppCompatActivity implements CompoundButton.OnCheckedChangeListener, Response.Listener<String>, Response.ErrorListener {
    private Switch activateLoaderSwitch;
    private View loadingIndicator;
    private TableLayout resultsTable;
    private Timer readerTimer;
    private Handler doLoadDataHandler;
    private boolean loading;
    private RequestQueue requestQueue;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        loadingIndicator = findViewById(R.id.loadingProgress);
        loadingIndicator.setVisibility(View.INVISIBLE);
        activateLoaderSwitch = findViewById(R.id.activateLoaderSwitch);
        resultsTable = findViewById(R.id.resultsTable);
        activateLoaderSwitch.setOnCheckedChangeListener(this);
        MainActivity outer = this;
        doLoadDataHandler = new Handler(this.getMainLooper()) {
            @Override
            public void handleMessage(Message msg) {
                outer.doLoadData();
            }
        };
        requestQueue = Volley.newRequestQueue(this);
    }
    @Override
    public void onCheckedChanged(CompoundButton buttonView, boolean isChecked) {
        if (buttonView == activateLoaderSwitch) {
            if (isChecked) {
                readerTimer = new Timer();
                readerTimer.scheduleAtFixedRate(new TimerTask() {
                    @Override
                    public void run() {
                        doLoadDataHandler.obtainMessage().sendToTarget();
                    }
                }, 0, 5000);
            } else {
                readerTimer.cancel();
                readerTimer = null;
            }
        }
    }
    private void doLoadData() {
        if (this.loading) {
            return;
        }
        this.loading = true;
        loadingIndicator.setVisibility(View.VISIBLE);
        String url = "YOUR_CLOUD_FUNCTION_URL";
        this.requestQueue.add(new StringRequest(Request.Method.GET, url, this, this));
    }
    @Override
    public void onResponse(String response) {
        try {
            resultsTable.removeAllViews();
            JSONArray activities = new JSONArray(response);
            JSONObject lastActivity = null;
            Date activityPeriodStart = null;
            for (int i = 0; i < activities.length(); i++) {
                JSONObject activity = activities.getJSONObject(i);
                System.out.println(activity);
                if (lastActivity != null) {
                    if (!lastActivity.getString("activity").equalsIgnoreCase(activity.getString("activity"))) {
                        appendActivityPeriod(activityPeriodStart, new Date(activity.getLong("timestamp")), lastActivity.getString("activity"));
                        activityPeriodStart = new Date(activity.getLong("timestamp"));
                    }
                } else {
                    activityPeriodStart = new Date(activity.getLong("timestamp"));
                }
                lastActivity = activity;
            }
        } catch (JSONException e) {
            e.printStackTrace();
        } finally {
            loadingIndicator.setVisibility(View.INVISIBLE);
            this.loading = false;
        }
    }
    @Override
    public void onErrorResponse(VolleyError error) {
        System.out.println(error.getMessage());
        loadingIndicator.setVisibility(View.INVISIBLE);
        this.loading = false;
    }
    private void appendActivityPeriod(Date periodStart, Date periodEnd, String activity) {
        TableRow row = new TableRow(this.getBaseContext());
        DateFormat fmt = DateFormat.getDateTimeInstance();
        TextView startTimestamp = new TextView(this.getBaseContext());
        startTimestamp.setText(fmt.format(periodStart));
        row.addView(startTimestamp);
        Space s = new Space(this.getBaseContext());
        s.setMinimumWidth(32);
        row.addView(s);
        TextView endTimestamp = new TextView(this.getBaseContext());
        endTimestamp.setText(fmt.format(periodEnd));
        row.addView(endTimestamp);
        Space s2 = new Space(this.getBaseContext());
        s2.setMinimumWidth(32);
        row.addView(s2);
        TextView activityText = new TextView(this.getBaseContext());
        activityText.setText(activity);
        row.addView(activityText);
        resultsTable.addView(row);
    }
}
```

Update `activity_main.xml`:
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">
    <ProgressBar
        android:id="@+id/loadingProgress"
        style="?android:attr/progressBarStyle"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginStart="182dp"
        android:layout_marginTop="14dp"
        android:layout_marginEnd="181dp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />
    <ScrollView
        android:id="@+id/scrollView2"
        android:layout_width="409dp"
        android:layout_height="667dp"
        app:layout_constraintBottom_toTopOf="@+id/activateLoaderSwitch"
        app:layout_constraintTop_toBottomOf="@+id/loadingProgress"
        app:layout_constraintVertical_bias="0.0"
        tools:layout_editor_absoluteX="1dp">
        <TableLayout
            android:id="@+id/resultsTable"
            android:layout_width="match_parent"
            android:layout_height="wrap_content" />
    </ScrollView>
    <Switch
        android:id="@+id/activateLoaderSwitch"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginStart="133dp"
        android:layout_marginEnd="133dp"
        android:layout_marginBottom="16dp"
        android:minHeight="48dp"
        android:text="Activate Loader"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent" />
</androidx.constraintlayout.widget.ConstraintLayout>
```

Add internet permission to `AndroidManifest.xml`:
```xml
<uses-permission android:name="android.permission.INTERNET" />
```

Build and run the app. Toggle the switch to fetch and display activity data. Simulate activities (e.g., walking, running) by shaking the device to see updates in the table.
