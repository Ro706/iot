# ESP32 DHT 

```c
#include <WiFi.h>
#include <HTTPClient.h>
#include "DHT.h"

#define DHTPIN 4       // GPIO where the DHT sensor is connected
#define DHTTYPE DHT11  // Change to DHT22 if using DHT22
DHT dht(DHTPIN, DHTTYPE);

// Wi-Fi credentials
const char* ssid = "YOUR_WIFI_SSID";
const char* password = "YOUR_WIFI_PASSWORD";

// ThingSpeak settings
const char* server = "http://api.thingspeak.com/update";
String apiKey = "YOUR_THINGSPEAK_API_KEY";

void setup() {
    Serial.begin(115200);
    dht.begin();

    WiFi.begin(ssid, password);
    Serial.print("Connecting to WiFi");

    while (WiFi.status() != WL_CONNECTED) {
        delay(500);
        Serial.print(".");
    }
    Serial.println(" Connected!");
}

void loop() {
    if (WiFi.status() == WL_CONNECTED) {
        float temp = dht.readTemperature();
        float hum = dht.readHumidity();

        if (isnan(temp) || isnan(hum)) {
            Serial.println("Failed to read from DHT sensor!");
            return;
        }

        Serial.print("Temperature: ");
        Serial.print(temp);
        Serial.print(" °C, Humidity: ");
        Serial.print(hum);
        Serial.println(" %");

        HTTPClient http;
        String url = server + "?api_key=" + apiKey + "&field1=" + String(temp) + "&field2=" + String(hum);
        
        http.begin(url);
        int httpResponseCode = http.GET();
        
        if (httpResponseCode > 0) {
            Serial.println("Data sent to ThingSpeak successfully");
        } else {
            Serial.print("Error sending data: ");
            Serial.println(httpResponseCode);
        }
        
        http.end();
    } else {
        Serial.println("WiFi Disconnected");
    }

    delay(15000);  // Send data every 15 seconds
}


```

## connection
![image](https://github.com/user-attachments/assets/ae1ea700-4eaf-49d1-b4ad-9b96f21ba586)

