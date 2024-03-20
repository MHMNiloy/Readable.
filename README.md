# Readable.
GSM WITH SENSORS
// MAHMUD's sensor code

#include <SoftwareSerial.h>

// Gas sensor
const int gasSensorPin = A0;

// Water sensor
const int waterSensorPin = 2;

// Vibration sensor
const int vibrationSensorPin = 3;

// Temperature sensor
const int tempSensorPin = A1;

// GSM module
const int gsmRX = 9;
const int gsmTX = 10;

SoftwareSerial gsmModule(gsmRX, gsmTX);

void setup() {
  Serial.begin(9600);
  gsmModule.begin(9600);

  pinMode(waterSensorPin, INPUT);
  pinMode(vibrationSensorPin, INPUT);
}

void loop() {
  int gasValue = analogRead(gasSensorPin);
  int waterValue = digitalRead(waterSensorPin);
  int vibrationValue = digitalRead(vibrationSensorPin);
  int tempValue = analogRead(tempSensorPin);

  if (gasValue == HIGH) {
    Serial.println("GAS Detected!");
    sendSMS("GAS detected!");
    }

    else{
      Serial.println("NO GAS DETECTED");
      // sendSMS("NO GAS DETECTED")
    }
  
  
  if (waterValue == HIGH) {
    Serial.println("Water Detected!");
    sendSMS("Water detected!");
    }

    else{
      Serial.println("NO Water Detected");
      // sendSMS("NO WATER DETECTED")
    }
  

 if (vibrationValue == HIGH) {
    Serial.println("Vibration Detected!");
    sendSMS("Vibration detected!");
    }

    else{
      Serial.println("NO Vibration DETECTED");
      // sendSMS("NO Vibration DETECTED")
    }
  
  if (tempValue == HIGH) {
    Serial.println("Temperature detected!");
    sendSMS("Temperature  detected!");
    }

    else{
      Serial.println("NO Temperature DETECTED");
      // sendSMS("NO Temperature DETECTED")
    }
  
  delay(5000);  // Adjust the delay based on your needs
}

void sendSMS(String message) {
  gsmModule.println("AT");
  delay(5000);
  gsmModule.println("AT+CMGF=1");
  delay(5000);
  gsmModule.println("AT+CMGS=\"+***********\""); // Replace with the recipient's phone number
  delay(5000);
  gsmModule.print(message);
  delay(5000);
  gsmModule.write(26);
  delay(5000);
}
