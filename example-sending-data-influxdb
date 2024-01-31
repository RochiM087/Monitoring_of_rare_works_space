
  #if defined(ESP32)
  #include <WiFiMulti.h>
  WiFiMulti wifiMulti;
  #define DEVICE "ESP32"
  #elif defined(ESP8266)
  #include <ESP8266WiFiMulti.h>
  ESP8266WiFiMulti wifiMulti;
  #define DEVICE "ESP8266"
  #endif
  
  #include <InfluxDbClient.h>
  #include <InfluxDbCloud.h>


  
  // WiFi AP SSID
  #define WIFI_SSID "wifiname"
  // WiFi password
  #define WIFI_PASSWORD "pwd"
  
  #define INFLUXDB_URL "url"
  #define INFLUXDB_TOKEN "token"
  #define INFLUXDB_ORG "org"
  #define INFLUXDB_BUCKET "bkt"
//  Point sensor("ESP32_user");

#define LIGHTSENSORPIN 13 //Ambient light sensor reading

const int HCSR501 = 4; // pino do sensor HCSR501 ligado ao pino 2 do ESP32
const int LED = 2; // pino do LED ligado ao pino 4 do ESP32


  // Time zone info
  #define TZ_INFO "UTC-3"
  
  // Declare InfluxDB client instance with preconfigured InfluxCloud certificate
//  InfluxDBClient client(INFLUXDB_URL, INFLUXDB_ORG, INFLUXDB_BUCKET, INFLUXDB_TOKEN, InfluxDbCloud2CACert);
  

void setup() {
//  pinMode(HCSR501, INPUT); // Configura o pino do sensor como entrada
//  pinMode(LED, OUTPUT); // Configura o pino do LED como saída
  pinMode(LIGHTSENSORPIN,  INPUT); 
  Serial.begin(9600);

 // Setup wifi
    WiFi.mode(WIFI_STA);
    wifiMulti.addAP(WIFI_SSID, WIFI_PASSWORD);
  
    Serial.print("Connecting to wifi");
    while (wifiMulti.run() != WL_CONNECTED) {
      Serial.print(".");
      delay(100);
    }
    Serial.println();
  
    // Accurate time is necessary for certificate validation and writing in batches
    // We use the NTP servers in your area as provided by: https://www.pool.ntp.org/zone/
    // Syncing progress and the time will be printed to Serial.
    timeSync(TZ_INFO, "pool.ntp.org", "time.nis.gov");
  
  
//    // Check server connection
//    if (client.validateConnection()) {
//      Serial.print("Connected to InfluxDB: ");
//      Serial.println(client.getServerUrl());
//    } else {
//      Serial.print("InfluxDB connection failed: ");
//      Serial.println(client.getLastErrorMessage());
//    }
//
//    // Add tags to the data point
//    sensor.addTag("device", DEVICE);
//    sensor.addTag("SSID", WiFi.SSID());
    


}

void loop() {

 
  float reading = analogRead(LIGHTSENSORPIN)*3.3/1024.0; //Read light level
//float reading = analogRead(LIGHTSENSORPIN);
  float amps = reading *100;
  float lux = amps * 2.0;

  Serial.print(reading);      
  Serial.println(lux);                    //Display reading in serial monitor


//  int valor = digitalRead(HCSR501); // Lê o valor do pino do sensor
//  if (valor == HIGH) {
//    // Movimento detectado
//    digitalWrite(LED, HIGH); // Ligar o LED
//    Serial.println("Movimento detectado"); // Mostrar mensagem no terminal
//  } else {
//    // Não há movimento detectado
//    digitalWrite(LED, LOW); // Desligar o LED
//    Serial.println("Sem Movimento!");
//  }
  


  
    // Clear fields for reusing the point. Tags will remain the same as set above.
//    sensor.clearFields();
  
    // Store measured value into point
    // Report RSSI of currently connected network
    //sensor.addField("tempC", grausC);
//    sensor.addField("Luminosity_B", lux);
//    sensor.addField("Luminosity_B", reading);
//    sensor.addField("presenca", valor);
    
    // Print what are we exactly writing
//    Serial.print("Writing: ");
//    Serial.println(sensor.toLineProtocol());
    
  
    // Check WiFi connection and reconnect if needed
    if (wifiMulti.run() != WL_CONNECTED) {
      Serial.println("Wifi connection lost");
    }
  
//    // Write point
//    if (!client.writePoint(sensor)) {
//      Serial.print("InfluxDB write failed: ");
//      Serial.println(client.getLastErrorMessage());
//    }
//  
//    Serial.println("Waiting 1 second");
    delay(500);
}
