---
title: "Electrical Setup"
date: 2025-07-23
---

## Software

- Install [Arduino IDE](https://www.arduino.cc/en/software/)

## L293D Motor Driver

- Wire the [circuit](https://www.tinkercad.com/things/ehT2Jv0teTn-l293d-motor-driver?sharecode=ptKgyQ0MTZuHiNs5623u1GnzgUm6TEFuzgF3rDnG1LI) for the motor driver.

![picture 0](https://i.imgur.com/1gINfhA.png)  

- Upload the following `L293D_motor_driver.ino` sketch to the Arduino 

```javascript
// L293D Motor Driver pins for right motor (Motor A)
const int ENA = 11;    // PWM speed control for right motor
const int IN1 = 13;    // Direction control 1 for right motor
const int IN2 = 12;    // Direction control 2 for right motor
 
// L293D Motor Driver pins for left motor (Motor B)
const int ENB = 10;    // PWM speed control for left motor
const int IN3 = 8;     // Direction control 1 for left motor
const int IN4 = 9;     // Direction control 2 for left motor
 
const int switchPin = 7; // Switch to turn robot on/off
 
int motorSpeed = 0; // Starting motor speed
 
void setup() {
    pinMode(switchPin, INPUT_PULLUP);
 
    pinMode(IN1, OUTPUT);
    pinMode(IN2, OUTPUT);
    pinMode(ENA, OUTPUT);
 
    pinMode(IN3, OUTPUT);
    pinMode(IN4, OUTPUT);
    pinMode(ENB, OUTPUT);
 
    Serial.begin(9600);
    Serial.println("To infinity and beyond!");
    motorSpeed = 255;
    Serial.print("Motor Speed: ");
    Serial.println(motorSpeed);
}
 
void loop() {
    motorSpeed = 255;
    // if (digitalRead(switchPin) == LOW) { // Switch ON (pressed)
    if (digitalRead(switchPin) == HIGH) { // Switch OFF 
        rightMotor(motorSpeed);
        leftMotor(motorSpeed);
    } else { // Switch OFF
        rightMotor(0);
        leftMotor(0);
    }
}
 
void rightMotor(int speed) {
    if (speed > 0) {
        digitalWrite(IN1, HIGH);
        digitalWrite(IN2, LOW);
    } else if (speed < 0) {
        digitalWrite(IN1, LOW);
        digitalWrite(IN2, HIGH);
    } else {
        digitalWrite(IN1, LOW);
        digitalWrite(IN2, LOW);
    }
    analogWrite(ENA, abs(speed));
}
 
void leftMotor(int speed) {
    if (speed > 0) {
        digitalWrite(IN3, HIGH);
        digitalWrite(IN4, LOW);
    } else if (speed < 0) {
        digitalWrite(IN3, LOW);
        digitalWrite(IN4, HIGH);
    } else {
        digitalWrite(IN3, LOW);
        digitalWrite(IN4, LOW);
    }
    analogWrite(ENB, abs(speed));
}
```