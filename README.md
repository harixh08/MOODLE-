# harish-212223060
# IOT-BASED-GARBAGE-MONITORING-SYSTEM-

# Tinkercard link:
https://www.tinkercad.com/things/aubj0bRwZN3/editel

## Objective of the project:
The objective of the IoT-based Garbage Monitoring System is to automate waste level detection in bins and notify the concerned authority when the bin is nearly full. This helps maintain cleanliness and optimize waste collection routes, saving both time and resources.

## Components used:
Arduino UNO: Acts as the main controller.
Ultrasonic Sensor (HC-SR04): Measures distance between the garbage level and the bin lid to determine fullness.
Servo Motor: Automatically opens or closes the bin lid.
Buzzer: Provides a local alert when the bin is full.
IoT Module (ESP8266 / Wi-Fi): Sends data to a cloud dashboard for real-time monitoring.

## Working Principle:
The ultrasonic sensor continuously measures the distance from the top of the bin to the waste level. If the measured distance falls below a threshold (e.g., 10 cm), the system identifies that the bin is full. The Arduino then activates a buzzer for an alert and triggers the servo motor to open the lid. The data can also be transmitted to an IoT platform like ThingSpeak or Blynk for remote monitoring, allowing authorities to schedule timely waste collection.

## IoT Application and Benefits:
Integrating IoT enables real-time monitoring of waste bins across various locations. When bins reach their threshold level, automatic notifications can be sent to municipal departments. This prevents overflowing bins, reduces manual inspection, and supports efficient waste management systems. The solution promotes cleaner environments, cost savings, and better public hygiene.

Overall, the IoT-based Garbage Monitoring System exemplifies how smart technology can address urban sanitation challenges efficiently.

## Block Diagram :
 <img width="432" height="426" alt="image" src="https://github.com/user-attachments/assets/cb1832b4-687e-41ba-a263-346464fda4b8" />

## Block Diagram Description

Main blocks:
Arduino UNO: Central controller that reads sensor data and controls the servo & buzzer.
Ultrasonic Sensor (HC-SR04): Detects the garbage level inside the bin.
Servo Motor: Opens the lid when garbage is detected.
Buzzer: Provides an alert when the bin is full.
IoT Module (e.g., NodeMCU or ESP8266): Sends bin status data to a cloud platform (e.g., ThingSpeak or Blynk) for remote monitoring.

## Program:
```
// IoT Based Garbage Monitoring System
// Components: Arduino UNO, Ultrasonic Sensor (HC-SR04), Servo Motor, Buzzer

#include <Servo.h>

#define TRIG 9       // Ultrasonic sensor TRIG pin
#define ECHO 10      // Ultrasonic sensor ECHO pin
#define BUZZER 8     // Buzzer pin
#define SERVO_PIN 6  // Servo motor pin

Servo servoMotor;

void setup() {
  Serial.begin(9600);
  pinMode(TRIG, OUTPUT);
  pinMode(ECHO, INPUT);
  pinMode(BUZZER, OUTPUT);
  servoMotor.attach(SERVO_PIN);

  servoMotor.write(0); // Bin lid closed initially
  Serial.println("Garbage Monitoring System Initialized");
}

void loop() {
  long duration;
  int distance;

  // Send ultrasonic pulse
  digitalWrite(TRIG, LOW);
  delayMicroseconds(2);
  digitalWrite(TRIG, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG, LOW);

  // Measure the echo pulse
  duration = pulseIn(ECHO, HIGH);
  distance = duration * 0.034 / 2; // Convert to centimeters

  Serial.print("Distance: ");
  Serial.println(distance);

  // If garbage level is high (less than 10 cm from top)
  if (distance < 10) {
    digitalWrite(BUZZER, HIGH); // Alert buzzer
    servoMotor.write(90);       // Open lid
    delay(2000);
    servoMotor.write(0);        // Close lid
    delay(1000);
  } else {
    digitalWrite(BUZZER, LOW);
    servoMotor.write(0);        // Keep lid closed
  }

  delay(1000);
}
```
## IoT Application and Benefits:
Integrating IoT enables real-time monitoring of waste bins across various locations. When bins reach their threshold level, automatic notifications can be sent to municipal departments. This prevents overflowing bins, reduces manual inspection, and supports efficient waste management systems. The solution promotes cleaner environments, cost savings, and better public hygiene.

Overall, the IoT-based Garbage Monitoring System exemplifies how smart technology can address urban sanitation challenges efficiently.

## Output:
<img width="1915" height="873" alt="image" src="https://github.com/user-attachments/assets/99aa29f2-8b9c-416c-b058-27d1d733bcb1" />

## Result :
This project shows how IoT and Arduino can be used to make waste management smarter and easier. The system checks the garbage level in a bin using an ultrasonic sensor and alerts when the bin is full. It helps reduce manual work, keeps the surroundings clean, and makes garbage collection more efficient.

By adding IoT features, the bin’s status can be viewed online, which helps in better planning and quick action. Overall, this project is a simple and useful step toward building cleaner and smarter cities.


