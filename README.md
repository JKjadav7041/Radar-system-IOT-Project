# 📡 Arduino Radar System using Ultrasonic Sensor & Servo Motor

## 🚀 Project Overview
This project demonstrates a Radar System using Arduino Uno, where an ultrasonic sensor scans the surroundings by rotating with a servo motor and detects objects in real-time.

The system measures distance at different angles and sends the data to the Serial Monitor / Processing IDE to visualize radar-like scanning.

---

## 🛠 Components Required

- Arduino Uno
- Ultrasonic Sensor (HC-SR04)
- Servo Motor (SG90)
- Jumper Wires
- Breadboard

---

## 🔧 Circuit Connections

### Ultrasonic Sensor (HC-SR04)

| Sensor Pin | Arduino Pin |
|------------|------------|
| VCC | 5V |
| GND | GND |
| TRIG | Pin 10 |
| ECHO | Pin 11 |

### Servo Motor (SG90)

| Servo Wire | Arduino Pin |
|------------|------------|
| Red | 5V |
| Brown/Black | GND |
| Orange/Yellow (Signal) | Pin 12 |

---

## 📊 Circuit Diagram

(Add your circuit image here)

Example:
![Circuit Diagram](images/circuit_diagram.png)

---

## 💻 Working Principle

1. The servo motor rotates from 15° to 165°.
2. At each angle:
   - The ultrasonic sensor sends a sound pulse.
   - It measures the echo return time.
   - Distance is calculated using:

Distance = (Duration × 0.034) / 2

3. The angle and distance are sent to Serial Monitor.
4. The data can be visualized in Processing IDE as a radar display.

---

## 🧠 Arduino Code

```cpp
#include <Servo.h>

const int trigPin = 10;
const int echoPin = 11;

long duration;
int distance;

Servo myServo;

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  Serial.begin(9600);
  myServo.attach(12);
}

void loop() {
  for(int i=15;i<=165;i++){  
    myServo.write(i);
    delay(30);
    distance = calculateDistance();
    Serial.print(i);
    Serial.print(",");
    Serial.print(distance);
    Serial.print(".");
  }

  for(int i=165;i>15;i--){  
    myServo.write(i);
    delay(30);
    distance = calculateDistance();
    Serial.print(i);
    Serial.print(",");
    Serial.print(distance);
    Serial.print(".");
  }
}

int calculateDistance(){ 
  digitalWrite(trigPin, LOW); 
  delayMicroseconds(2);

  digitalWrite(trigPin, HIGH); 
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2;
  return distance;
}
```

---

## 📈 Output Format

Angle,Distance.

Example:
90,25.

Where:
- 90 = Angle in degrees
- 25 = Distance in cm

---

## 🎯 Applications

- Obstacle Detection
- Radar Simulation
- Robotics Navigation
- Smart Parking System
- Security Scanning

---

## 🔮 Future Improvements

- Add LCD Display
- Add Buzzer Alert
- Wireless Monitoring using ESP8266
- Web Dashboard Integration

---

## 👨‍💻 Author

Jivraj Jadav 
Computer Engineer | IoT Developer
