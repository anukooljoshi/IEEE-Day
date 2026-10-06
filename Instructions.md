# Arduino Sandbox

Welcome to the Arduino Sandbox! This guide introduces the basics of Arduino programming and wiring, followed by simple circuits that you can build and modify yourself.

The goal is to learn by experimenting. Start with the basic examples, then change the code and see what happens.

---

## Table of Contents

1. [Getting Started](#getting-started)
2. [Arduino Programming Basics](#arduino-programming-basics)
3. [Basic Wiring](#basic-wiring)
4. [Circuit 1: Blinking LED](#circuit-1-blinking-led)
5. [Circuit 2: Button and LED](#circuit-2-button-and-led)
6. [Circuit 3: Potentiometer and LED](#circuit-3-potentiometer-and-led)
7. [Circuit 4: Photoresistor](#circuit-4-photoresistor)
8. [Circuit 5: RGB LED](#circuit-5-rgb-led)
9. [Circuit 6: Servo Motor](#circuit-6-servo-motor)
10. [Circuit 7: Ultrasonic Sensor](#circuit-7-ultrasonic-sensor)
11. [Beginner Challenges](#beginner-challenges)

---

# Getting Started

## What is an Arduino?

An Arduino is a small programmable circuit board that can read inputs from sensors and control electronic components such as LEDs, motors, and servos.

You write a program on your computer and upload it to the Arduino. The Arduino then runs the program.

### What you will need

* Arduino board
* USB cable
* Breadboard
* Jumper wires
* LEDs
* Resistors
* Push buttons
* Potentiometer
* Photoresistor
* Servo motor
* Ultrasonic sensor

---

# Arduino Programming Basics

Most Arduino programs have two main sections:

```cpp
void setup() {
  // Runs once
}

void loop() {
  // Runs repeatedly
}
```

## `setup()`

Anything inside `setup()` runs once when the Arduino starts.

For example:

```cpp
void setup() {
  pinMode(13, OUTPUT);
}
```

This tells the Arduino that pin 13 will be used as an output.

## `loop()`

Anything inside `loop()` runs repeatedly.

```cpp
void loop() {
  digitalWrite(13, HIGH);
  delay(1000);

  digitalWrite(13, LOW);
  delay(1000);
}
```

This turns an LED on for one second and then off for one second.

---

## Common Arduino Commands

| Command            | Purpose                                  |
| ------------------ | ---------------------------------------- |
| `pinMode()`        | Sets a pin as an input or output         |
| `digitalWrite()`   | Turns a digital output HIGH or LOW       |
| `digitalRead()`    | Reads a digital input                    |
| `analogRead()`     | Reads an analog input from 0–1023        |
| `analogWrite()`    | Outputs PWM from 0–255                   |
| `delay()`          | Pauses the program                       |
| `Serial.println()` | Prints information to the Serial Monitor |

### `pinMode()`

Sets a pin as an input or output.

```cpp
pinMode(13, OUTPUT);
pinMode(2, INPUT);
```

Common options:

* `OUTPUT` — sends a signal
* `INPUT` — reads a signal
* `INPUT_PULLUP` — input using the Arduino's internal pull-up resistor

### `digitalWrite()`

Turns a digital output on or off.

```cpp
digitalWrite(13, HIGH);
digitalWrite(13, LOW);
```

* `HIGH` = ON
* `LOW` = OFF

### `digitalRead()`

Reads a digital input.

```cpp
int buttonState = digitalRead(2);
```

The result will normally be `HIGH` or `LOW`.

### `analogRead()`

Reads an analog input.

```cpp
int sensorValue = analogRead(A0);
```

Arduino analog inputs normally return a value from `0` to `1023`.

### `analogWrite()`

Controls PWM output.

```cpp
analogWrite(9, 128);
```

The value can range from `0` to `255`.

### `delay()`

Pauses the program.

```cpp
delay(1000);
```

The value is in milliseconds.

* `1000` = 1 second
* `500` = 0.5 seconds
* `100` = 0.1 seconds

---

# Basic Wiring

Before building a circuit, make sure you understand how your breadboard is connected.

## Breadboard Basics

On most breadboards:

* Holes in the same row are electrically connected.
* The power rails are commonly used for `5V` and `GND`.
* Jumper wires connect different parts of the circuit.
* The Arduino and your circuit should share the same `GND`.

### Basic circuit path

For many circuits, the basic path is:

```text
Arduino Output → Component → GND
```

For example:

```text
Pin 13 → Resistor → LED → GND
```

## Important Safety Rules

* Always check your wiring before powering the circuit.
* LEDs should use a current-limiting resistor.
* Do not connect an Arduino output directly to `5V` or `GND`.
* Make sure components are connected to the correct pins.
* If a circuit does not work, disconnect power and check your wiring first.

---

# Circuit 1: Blinking LED

## Parts

* Arduino
* LED
* 220–330 Ω resistor
* Jumper wires
* Breadboard

## Wiring

```text
Arduino Pin 13
      |
   Resistor
      |
     LED
      |
     GND
```

The LED's longer leg is normally the positive side.

## Code

```cpp
void setup() {
  pinMode(13, OUTPUT);
}

void loop() {
  digitalWrite(13, HIGH);
  delay(1000);

  digitalWrite(13, LOW);
  delay(1000);
}
```

## Try It

Change the delay:

```cpp
delay(200);
```

How does this change the blinking speed?

---

# Circuit 2: Button and LED

Use a button to control an LED.

## Parts

* Arduino
* Push button
* LED
* 220–330 Ω resistor
* Jumper wires
* Breadboard

## Wiring

### Button

```text
Pin 2 → Button → GND
```

### LED

```text
Pin 13 → Resistor → LED → GND
```

We will use `INPUT_PULLUP`, so an external resistor is not required for the button.

## Code

```cpp
void setup() {
  pinMode(2, INPUT_PULLUP);
  pinMode(13, OUTPUT);
}

void loop() {
  int buttonState = digitalRead(2);

  if (buttonState == LOW) {
    digitalWrite(13, HIGH);
  } else {
    digitalWrite(13, LOW);
  }
}
```

When the button is pressed, pin 2 reads `LOW` and the LED turns on.

---

# Circuit 3: Potentiometer and LED

Use a potentiometer to control LED brightness.

## Parts

* Arduino
* Potentiometer
* LED
* 220–330 Ω resistor
* Jumper wires

## Wiring

### Potentiometer

```text
5V  → Outer Pin
A0  → Middle Pin
GND → Outer Pin
```

### LED

```text
Pin 9 → Resistor → LED → GND
```

## Code

```cpp
void setup() {
  pinMode(9, OUTPUT);
}

void loop() {
  int sensorValue = analogRead(A0);
  int brightness = map(sensorValue, 0, 1023, 0, 255);

  analogWrite(9, brightness);
}
```

Turn the potentiometer and observe how the LED brightness changes.

---

# Circuit 4: Photoresistor

A photoresistor changes its resistance depending on the amount of light.

## Parts

* Arduino
* Photoresistor
* 10 kΩ resistor
* LED
* 220–330 Ω resistor
* Jumper wires

## Wiring

Create a voltage divider:

```text
5V
 |
Photoresistor
 |
 +------ A0
 |
10 kΩ Resistor
 |
GND
```

Connect the LED:

```text
Pin 9 → Resistor → LED → GND
```

## Code

```cpp
void setup() {
  pinMode(9, OUTPUT);
}

void loop() {
  int lightLevel = analogRead(A0);
  int brightness = map(lightLevel, 0, 1023, 0, 255);

  analogWrite(9, brightness);
}
```

## Try It

Cover the photoresistor with your hand.

You can also reverse the LED behavior:

```cpp
brightness = 255 - brightness;
```

---

# Circuit 5: RGB LED

An RGB LED contains three LEDs:

* Red
* Green
* Blue

By controlling each color individually, you can create many different colors.

## Parts

* Arduino
* RGB LED
* 3 × 220–330 Ω resistors
* Jumper wires

## Wiring

For a common-cathode RGB LED:

```text
Red   → Resistor → Pin 9
Green → Resistor → Pin 10
Blue  → Resistor → Pin 11
Common → GND
```

## Code

```cpp
void setup() {
  pinMode(9, OUTPUT);
  pinMode(10, OUTPUT);
  pinMode(11, OUTPUT);
}

void loop() {
  analogWrite(9, 255);
  analogWrite(10, 0);
  analogWrite(11, 0);
}
```

This produces red.

Try changing the values:

```cpp
analogWrite(9, 0);
analogWrite(10, 255);
analogWrite(11, 0);
```

This produces green.

---

# Circuit 6: Servo Motor

A servo motor can be controlled to move to a specific angle.

## Parts

* Arduino
* Servo motor
* Jumper wires

## Wiring

```text
Servo VCC     → 5V
Servo GND     → GND
Servo Signal  → Pin 9
```

## Code

```cpp
#include <Servo.h>

Servo myServo;

void setup() {
  myServo.attach(9);
}

void loop() {
  myServo.write(0);
  delay(1000);

  myServo.write(90);
  delay(1000);

  myServo.write(180);
  delay(1000);
}
```

The servo moves between 0°, 90°, and 180°.

---

# Circuit 7: Ultrasonic Sensor

An ultrasonic sensor can measure the distance between the sensor and an object.

## Parts

* Arduino
* HC-SR04 ultrasonic sensor
* Jumper wires

## Wiring

```text
VCC  → 5V
GND  → GND
TRIG → Pin 9
ECHO → Pin 10
```

## Code

```cpp
void setup() {
  Serial.begin(9600);

  pinMode(9, OUTPUT);
  pinMode(10, INPUT);
}

void loop() {
  digitalWrite(9, LOW);
  delayMicroseconds(2);

  digitalWrite(9, HIGH);
  delayMicroseconds(10);
  digitalWrite(9, LOW);

  long duration = pulseIn(10, HIGH);
  float distance = duration * 0.034 / 2;

  Serial.println(distance);

  delay(100);
}
```

Open the **Serial Monitor** to see the distance in centimeters.

---

# Beginner Challenges

Once you have completed the basic circuits, try modifying them.

## LED

* Make the LED blink faster.
* Make the LED blink slower.
* Create a blinking pattern.
* Control two LEDs.

## Button

* Make the button toggle the LED.
* Use two buttons to control two LEDs.
* Make the LED blink while the button is held.

## Potentiometer

* Control LED brightness.
* Control the speed of an LED.
* Use the potentiometer to control a servo.

## Photoresistor

* Turn an LED on when it gets dark.
* Make the LED brighter as the room gets darker.
* Create an automatic night light.

## Servo

* Use a potentiometer to control the servo.
* Use a button to move the servo between two positions.
* Use the ultrasonic sensor to control the servo.

## Ultrasonic Sensor

* Turn on an LED when an object gets close.
* Make the LED brightness depend on distance.
* Use the sensor to control a servo.

---

# General Workflow

For each sandbox activity, follow these steps:

1. **Identify the components**
   Determine which components are being used.

2. **Build the circuit**
   Follow the wiring instructions.

3. **Read the code**
   Look at what each part of the program does.

4. **Upload the code**
   Connect your Arduino and upload the program.

5. **Test the circuit**
   Check whether it behaves as expected.

6. **Experiment**
   Change values in the code and see what happens.

7. **Complete the challenge**
   Try modifying the circuit or creating your own version.

---

# Have Fun!

The best way to learn Arduino is to **experiment**.

If something doesn't work, check:

* Is the Arduino connected?
* Is the correct board selected?
* Is the correct COM port selected?
* Are the wires connected correctly?
* Is the component oriented correctly?
* Are the correct pins being used?
* Did the code upload successfully?

Don't be afraid to change the code and see what happens!
