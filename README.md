# COZMOCLENCH ELECTRONICS 

## COMPONENTS NEEDED
NodeMCU ESP8266

Motor Driver L298N (x2)

300RPM DC Motors (x4)

12V Servo Motor (x3)

Arduino Mega (For Backup)

HC-06 (For Backup)

1k Resistors (x2)

## CIRCUIT DIAGRAM

![](https://github.com/meghang-101/CozmoClench/blob/main/CozmoClench02.PNG)

## CODE FOR MCU8200/ARDUINO MEGA

The Code is written according to the Pinout of the ESP8266

![](https://github.com/meghang-101/CozmoClench/blob/main/Capture.PNG)

[Code](https://github.com/meghang-101/CozmoClench/blob/main/esp8266_01.ino)

```python
#include <ESP8266WiFi.h>
#include <Servo.h>
#include <String.h>

Servo servo1;
Servo servo2;
Servo servo3;

const char* ssid = ""; //Add your WiFi SSID here
const char* password = ""; //Add your WiFi password here

char input = 0;
int data = 0;

#define MotorLeftPWM 16 //ENA pin on the L298N
#define MotorRightPWM 5 //ENB pin on the L298N
#define IN1 4 //IN1 pin on L298 Controls the direction of MotorLeft clockwise
#define IN2 0 //IN2 pin on L298 Controls the direction of MotorLeft anticlockwise
#define IN3 2 //IN3 pin on L298 Controls the direction of MotorRight clockwise
#define IN4 14 //IN4 pin on L298 Controls the direction of MotorRight anticlockwise
#define Servo1 12 //Signal for Servo1
#define Servo2 13 //Signal for Servo2
#define Servo3 15 //Signal for Servo3

void setup() {
  pinMode(IN1, OUTPUT);
  pinMode(IN2, OUTPUT);
  pinMode(IN3, OUTPUT);
  pinMode(IN4, OUTPUT);
  servo1.attach(Servo1);
  servo2.attach(Servo2);
  servo3.attach(Servo3);

  Serial.begin(11500);

  Serial.println();
  Serial.print("Wifi connecting");
  Serial.println();
  WiFi.begin(ssid, password);
  while (Wifi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  Serial.println();
  Serial.print("Conneted succesfully");

}

void loop() {
  if (Serial.available()) {
    input = Serial.read(); //Reads input from Serial monitor
    data = input.toInt(); //Converts input to integer data

    //FORWARD MOVEMENT
    if (data == 1) {
      while (data = 1) {
        digitalWrite(IN1, LOW);
        digitalWrite(IN2, HIGH);
        digitalWrite(IN3, HIGH);
        digitalWrite(IN4, LOW);
        for (int i=0; i<100, i=i+10) {
          digitalWrite(MotorLeftPWM, i);
          digitalWrite(MotorRightPWM, i);
        }
      }
    }

    //BACKWARD MOVEMENT
    if (data == 2) {
      while (data = 2) {
        digitalWrite(IN1, HIGH);
        digitalWrite(IN2, LOW);
        digitalWrite(IN3, LOW);
        digitalWrite(IN4, HIGH);
        for (int i=0; i<100, i=i+10) {
          digitalWrite(MotorLeftPWM, i);
          digitalWrite(MotorRightPWM, i);
        }
      }
    }  

    //TURN LEFT
    if (data == 3) {
      while (data = 3) {
        digitalWrite(IN1, HIGH);
        digitalWrite(IN2, LOW);
        digitalWrite(IN3, HIGH);
        digitalWrite(IN4, LOW);
        for (int i=0; i<100, i=i+10) {
          digitalWrite(MotorLeftPWM, i);
          digitalWrite(MotorRightPWM, i);
        }
      }
    }

    //TURN RIGHT
    if (data == 4){
      while (data = 4) {
        digitalWrite(IN1, LOW);
        digitalWrite(IN2, HIGH);
        digitalWrite(IN3, LOW);
        digitalWrite(IN4, HIGH);
        for (int i=0; i<100, i=i+10) {
          digitalWrite(MotorLeftPWM, i);
          digitalWrite(MotorRightPWM, i);
        }
      }
    }

    //SERVO 1 ACTUATION
    if (data == 5) {
      servo1.write(180);
    }
    if (data == 6) {
      servo1.write(0);
    }
    
    //SERVO 2 ACTUATION
    if (data == 7) {
      servo1.write(180);
    }
    if (data == 8) {
      servo1.write(0);
    }

    //SERVO 3 ACTUATION
    if (data == 9) {
      servo1.write(180);
    }
    if (data == 10) {
      servo1.write(0);
    }
    
  } 
  else {
    data = 0;
  }
}
```
