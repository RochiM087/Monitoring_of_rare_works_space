# Monitoring Rare_Works_Space_

![ESP32](https://img.shields.io/badge/ESP32-Device-blue)
![ESP8266](https://img.shields.io/badge/ESP8266-Device-blue)
![InfluxDB](https://img.shields.io/badge/InfluxDB-Database-green)
![WiFi](https://img.shields.io/badge/WiFi-Connection-orange)

## Table of Contents
- [Monitoring Rare_Works_Space_](#monitoring-rare_works_space_)
  - [Table of Contents](#table-of-contents)
  - [Device Configuration](#device-configuration)
  - [InfluxDB Communication](#influxdb-communication)
  - [Connection Details](#connection-details)
  - [Sensor Setup](#sensor-setup)
  - [Time Zone Configuration](#time-zone-configuration)
  - [Setup Function](#setup-function)
  - [Loop Function](#loop-function)

## Device Configuration

```cpp
#if defined(ESP32)
#include <WiFiMulti.h>
WiFiMulti wifiMulti;
#define DEVICE "ESP32"
#elif defined(ESP8266)
#include <ESP8266WiFiMulti.h>
ESP8266WiFiMulti wifiMulti;
#define DEVICE "ESP8266"
#endif
```
- Here we are performing some conditional checks to determine if we are compiling for ESP32 or ESP8266. Depending on that,
we include the appropriate libraries for multi WiFi connection and define a global variable wifiMulti that will be used
to manage multiple WiFi connections. We also define a macro DEVICE to identify the type of device.


## InfluxDB Communication

```cpp
#include <InfluxDbClient.h>
#include <InfluxDbCloud.h>
```
- Here are the includes of the necessary libraries to communicate with InfluxDB.

## Connection Details

```cpp
#define WIFI_SSID "SSID"
#define WIFI_PASSWORD "PWD"
#define INFLUXDB_URL "URL"
#define INFLUXDB_TOKEN "TOKEN"
#define INFLUXDB_ORG "ORG"
#define INFLUXDB_BUCKET "BUCKET"
```
- Here we define the details of the WiFi connection such as SSID and password, and also the details of the InfluxDB connection like URL, authentication token, organization, and bucket.

## Sensor Setup (EXAMPLE)

```cpp
#define LIGHTSENSORPIN 13 //Ambient light sensor reading
const int HCSR501 = 4; // pin of HCSR501 sensor connected to pin 2 of ESP32
const int LED = 2; // pin of LED connected to pin 4 of ESP32
```
- We define constants for the pins used by the light sensor, motion sensor (HCSR501), and LED. 


## Time Zone Configuration

```cpp
#define TZ_INFO "UTC-3"
```
- Here we define the time zone that will be used for time synchronization with NTP servers.


## Setup Function
```cpp
void setup() {
    pinMode(LIGHTSENSORPIN,  INPUT); 
    Serial.begin(9600);
    WiFi.mode(WIFI_STA);
    wifiMulti.addAP(WIFI_SSID, WIFI_PASSWORD);
    Serial.print("Connecting to wifi");
    while (wifiMulti.run() != WL_CONNECTED) {
        Serial.print(".");
        delay(100);
    }
    Serial.println();
    timeSync(TZ_INFO, "pool.ntp.org", "time.nis.gov");
}

```
- In the `setup()`, we set the pin of the light sensor as input, initialize serial communication, set the WiFi mode to station `(WIFI_STA)`, add the WiFi network, and wait until the connection is established. We also synchronize time with an NTP server.


## Loop Function
```cpp
void loop() {
    float reading = analogRead(LIGHTSENSORPIN) * 3.3 / 1024.0; //Read light level
    float amps = reading * 100;
    float lux = amps * 2.0;
    Serial.print(reading);      
    Serial.println(lux);                    //Display reading in serial monitor
    delay(500);
}
```
- In the `loop()`, we read the value of the light sensor using analogRead() and convert the value to volts. Then, we calculate the luminosity in lux based on the reading value. These values are printed on the serial monitor, and then a small delay of 500 milliseconds is added before the next iteration.

This example illustrates a basic sensor data acquisition process that can be applied to various IoT projects. By adapting this example, developers can integrate different types of sensors, customize data processing logic, and extend functionality, making it suitable for a wide range of applications.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

