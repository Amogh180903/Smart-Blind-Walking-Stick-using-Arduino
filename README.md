# Smart-Blind-Walking-Stick-using-Arduino
A cost-effective and functional walking stick designed to assist visually impaired individuals using Arduino and ultrasonic technology. It detects nearby obstacles and alerts the user via buzzer, LED, and vibrations.

### Objective:
To develop a smart walking stick that can alert visually impaired individuals to nearby obstacles, thereby helping them navigate safely and independently.

### Components Used:
	•	Arduino Uno
	•	HC-SR04 Ultrasonic Sensor
	•	Buzzer
	•	Vibration Motor
	•	LED with 220Ω resistor
	•	Jumper Wires
	•	PVC Pipe
	•	Battery Holder & Rechargeable Battery
	•	Cable Ties

### Working Principle:

The stick uses an ultrasonic sensor to detect obstacles up to a distance of 25 cm. When an object is detected:

	•	The buzzer beeps.
	•	The LED lights up.
	•	The vibration motor activates (inferred from report, although not coded in the current version).

These alerts notify the user of nearby obstructions, helping them avoid collisions.

### Circuit Diagram

![Circuit Diagram](Diagram.jpg)

### Arduino Code:
const int trigPin = 9;<br>
const int echoPin = 10;<br>
const int buzzer = 11;<br>
const int ledPin = 13;<br>

long duration;<br>
int distance;<br>
int safetyDistance;<br>

void setup() {<br>
  pinMode(trigPin, OUTPUT);<br>
  pinMode(echoPin, INPUT);<br>
  pinMode(buzzer, OUTPUT);<br>
  pinMode(ledPin, OUTPUT);<br>
  Serial.begin(9600);<br>
}<br>

void loop() {<br>
  digitalWrite(trigPin, LOW);<br>
  delayMicroseconds(2);<br>
  digitalWrite(trigPin, HIGH);<br>
  delayMicroseconds(10);<br>
  digitalWrite(trigPin, LOW);<br>

  duration = pulseIn(echoPin, HIGH);<br>
  distance = duration * 0.034 / 2;<br>
  safetyDistance = distance;<br>

  if (safetyDistance <= 25) {<br>
    digitalWrite(buzzer, HIGH);<br>
    digitalWrite(ledPin, HIGH);<br>
  } else {<br>
    digitalWrite(buzzer, LOW);<br>
    digitalWrite(ledPin, LOW);<br>
  }<br>

  Serial.print("Distance: ");<br>
  Serial.println(distance);<br>
}<br>

### Result:

When an obstacle is detected within 25 cm:

	•	The LED lights up,
	•	The buzzer beeps,
	•	And the user is alerted effectively.

No alert is triggered if the path is clear.
