# Cybersecurity 150 Lab

## Name of Project
ESP32 Send a message to WhatsApp

## Purpose
Create an ESP32 project using the ESP32

## Equipment
* [ESP32Wroom](https://www.amazon.com/Aideepen-ESP32-WROOM-Bluetooth-ESP32-CAM-MB-Arduino/dp/B08P2578LV/ref=sr_1_3?crid=4FY0ECFW0ZX7&keywords=ESP32+Cam&qid=1678902050&sprefix=esp32+cam%2Caps%2C240&sr=8-3)

* [USB Micro Data Cable](https://www.amazon.com/AmazonBasics-Male-Micro-Cable-Black/dp/B0711PVX6Z/ref=sr_1_1_sspa?keywords=micro+usb+data+cable&qid=1678902214&sprefix=Micro+USB+data+%2Caps%2C89&sr=8-1-spons&psc=1&spLa=ZW5jcnlwdGVkUXVhbGlmaWVyPUFaU0NaUVZHU1RFUlAmZW5jcnlwdGVkSWQ9QTA3NTA4MDVFVERCS01HVlgxM1YmZW5jcnlwdGVkQWRJZD1BMDE4NTE1NTIwWUdONkdWSzU1M1Amd2lkZ2V0TmFtZT1zcF9hdGYmYWN0aW9uPWNsaWNrUmVkaXJlY3QmZG9Ob3RMb2dDbGljaz10cnVl)

## Link to Documentation Followed
- [GitHub - martin-ger/esp32_nat_router](https://github.com/martin-ger/esp32_nat_router)
- https://randomnerdtutorials.com/esp8266-nodemcu-send-messages-whatsapp/
- https://www.callmebot.com/
##### Youtube Video 1:
https://studio.youtube.com/video/y71e6WVouvE/edit

##### Youtube Video 2: 

##### Other Links: https://api.callmebot.com/whatsapp.php?phone=[phone_number]&text=[message]&apikey=[your_apikey]


## Steps I followed
1. Add the phone number: to your Phone Contacts. (Name it as you wish) — please double-check the number on the CallMeBot website, because it sometimes changes.
2. Send the following message: “I allow callmebot to send me messages” to the new Contact created (using WhatsApp of course);
3. Wait until you receive the message “API Activated for your phone number. Your APIKEY is XXXXXX” from the bot
4. To send a message using the CallMeBot API you need to make a POST request to the following URL (but using your information):

   https://api.callmebot.com/whatsapp.php?phone=[phone_number]&text=[message]&apikey=[your_apikey]
5.
#include <WiFi.h>    
#include <HTTPClient.h>
#include <UrlEncode.h>

const char* ssid = "REPLACE_WITH_YOUR_SSID";
const char* password = "REPLACE_WITH_YOUR_PASSWORD";

// +international_country_code + phone number
// Portugal +351, example: +351912345678
String phoneNumber = "REPLACE_WITH_YOUR_PHONE_NUMBER";
String apiKey = "REPLACE_WITH_API_KEY";

void sendMessage(String message){

  // Data to send with HTTP POST
  String url = "https://api.callmebot.com/whatsapp.php?phone=" + phoneNumber + "&apikey=" + apiKey + "&text=" + urlEncode(message);    
  HTTPClient http;
  http.begin(url);

  // Specify content-type header
  http.addHeader("Content-Type", "application/x-www-form-urlencoded");
  
  // Send HTTP POST request
  int httpResponseCode = http.POST(url);
  if (httpResponseCode == 200){
    Serial.print("Message sent successfully");
  }
  else{
    Serial.println("Error sending the message");
    Serial.print("HTTP response code: ");
    Serial.println(httpResponseCode);
  }

  // Free resources
  http.end();
}

void setup() {
  Serial.begin(115200);

  WiFi.begin(ssid, password);
  Serial.println("Connecting");
  while(WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  Serial.println("");
  Serial.print("Connected to WiFi network with IP Address: ");
  Serial.println(WiFi.localIP());

  // Send Message to WhatsAPP
  sendMessage("Hello from ESP32!");
}

void loop() {
  
}
 

## Problems
Note your problems or errors here.  Google any error you may come across, and not what you tried (even if it does not work), and what was the final answer.

1. My challenge was that ESP32 couldn't get to connect to the WIFI. The project code couldn't send the final output to  the receiver, WhatsApp server. The problem was that WIFI wasn't in the Arduino library.
## Solutin

1. After downloading <WIFI.H> in the library my ESP32 was successfully connected to the receiver: AIP key. The final output message was received from ESP32 through callmebot: AIP key.
   Message (Hello from ESP32!).
