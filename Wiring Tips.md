# Arduino Wiring Guide

Before programming your Arduino, it is important to understand how to build a circuit on a breadboard.

This guide covers the basic wiring concepts you will need for the Arduino Sandbox.

---

# 1. What is a Breadboard?

A breadboard allows you to build circuits without soldering.

You can plug components and jumper wires directly into the holes on the breadboard.

The holes are internally connected in groups, allowing electricity to flow between components.

---

# 2. Breadboard Connections

A typical breadboard has two main types of connections:

### Power Rails

The long rails along the sides of the breadboard are commonly used for power.

```text
+  +  +  +  +  +  +  +  +  +  +  +
-  -  -  -  -  -  -  -  -  -  -  -
```

You can connect:

```text
Arduino 5V  →  + rail
Arduino GND →  - rail
```

Then components can use these rails for power and ground.

### Terminal Rows

The smaller groups of holes in the middle of the breadboard are connected together.

A typical layout looks like:

```text
a b c d e     f g h i j
● ● ● ● ●     ● ● ● ● ●
● ● ● ● ●     ● ● ● ● ●
● ● ● ● ●     ● ● ● ● ●
```

The five holes on one side of a row are connected.

The five holes on the other side are connected separately.

The center gap keeps the two sides electrically separated.

---

# 3. Connecting the Arduino

A common starting point is to connect power to the breadboard.

```text
Arduino 5V  ─────────→ Breadboard +
Arduino GND ─────────→ Breadboard -
```

Now components on the breadboard can connect to the Arduino's power and ground rails.

---

# 4. Digital Pins

Arduino digital pins can be used as inputs or outputs.

For example:

```text
Pin 13 → LED
Pin 2  → Button
```

In your code, you tell the Arduino what each pin does.

```cpp
pinMode(13, OUTPUT);
pinMode(2, INPUT);
```

---

# 5. Connecting an LED

An LED has two legs:

* **Longer leg** → positive/anode
* **Shorter leg** → negative/cathode

A typical LED circuit looks like:

```text
Arduino Pin
     |
  Resistor
     |
    LED
     |
    GND
```

For example:

```text
Pin 13 → 220Ω Resistor → LED → GND
```

## Why use a resistor?

The resistor limits the current flowing through the LED.

Without a resistor, too much current can flow through the LED and damage it.

---

# 6. Connecting a Button

A push button can be used as a digital input.

One simple setup uses the Arduino's internal pull-up resistor:

```text
Pin 2 → Button → GND
```

Then use:

```cpp
pinMode(2, INPUT_PULLUP);
```

When the button is:

* **Not pressed** → `HIGH`
* **Pressed** → `LOW`

Example:

```cpp
void setup() {
  pinMode(2, INPUT_PULLUP);
}

void loop() {
  int buttonState = digitalRead(2);

  if (buttonState == LOW) {
    // Button is pressed
  }
}
```

---

# 7. Connecting a Potentiometer

A potentiometer has three pins.

For a basic analog input:

```text
Outer Pin  → 5V
Middle Pin → A0
Outer Pin  → GND
```

The middle pin produces a voltage between 0V and 5V depending on the position of the potentiometer.

The Arduino can read this using:

```cpp
int value = analogRead(A0);
```

The result is normally between:

```text
0 → 1023
```

---

# 8. Connecting a Photoresistor

A photoresistor can be used with a resistor to create a voltage divider.

```text
5V
 |
Photoresistor
 |
 +------ A0
 |
10kΩ
 |
GND
```

The voltage at `A0` changes depending on the amount of light.

You can read it using:

```cpp
int lightLevel = analogRead(A0);
```

---

# 9. Connecting a Servo

A typical servo has three wires:

| Servo Wire | Connect To  |
| ---------- | ----------- |
| VCC        | 5V          |
| GND        | GND         |
| Signal     | Digital pin |

For example:

```text
Servo VCC    → 5V
Servo GND    → GND
Servo Signal → Pin 9
```

The signal wire is controlled by the Arduino.

---

# 10. Connecting an Ultrasonic Sensor

An HC-SR04 ultrasonic sensor has four pins:

| HC-SR04 | Arduino |
| ------- | ------- |
| VCC     | 5V      |
| GND     | GND     |
| TRIG    | Pin 9   |
| ECHO    | Pin 10  |

The Arduino sends a signal through `TRIG` and measures the returned signal through `ECHO`.

---

# 11. Analog vs. Digital Pins

## Digital Pins

Digital pins have two basic states:

```text
HIGH
LOW
```

They are useful for things such as:

* LEDs
* Buttons
* Digital sensors

Example:

```cpp
digitalWrite(13, HIGH);
```

## Analog Pins

Analog pins can measure a range of voltages.

On many Arduino boards, `analogRead()` returns:

```text
0 → 1023
```

They are useful for things such as:

* Potentiometers
* Photoresistors
* Analog sensors

Example:

```cpp
int value = analogRead(A0);
```

---

# 12. PWM Pins

Some digital pins support **PWM**, which can be used to simulate different output levels.

PWM pins are usually marked with a `~` symbol.

For example:

```text
~3
~5
~6
~9
~10
~11
```

PWM can be used for:

* LED brightness
* Motor speed
* Other variable outputs

Example:

```cpp
analogWrite(9, 128);
```

The value ranges from:

```text
0 → 255
```

---

# 13. Common Wiring Mistakes

If your circuit doesn't work, check these first.

### 1. Missing Ground

Make sure the Arduino and your circuit share the same ground.

```text
Arduino GND → Circuit GND
```

### 2. LED Installed Backwards

Try flipping the LED around.

### 3. No Resistor

Make sure LEDs have an appropriate resistor.

### 4. Wrong Arduino Pin

Make sure the physical pin matches the pin number in your code.

For example:

```cpp
digitalWrite(13, HIGH);
```

means the component must actually be connected to **pin 13**.

### 5. Button Orientation

Many push buttons connect opposite pairs of pins. Make sure the button is positioned correctly across the breadboard's center gap.

### 6. Loose Wires

Make sure jumper wires and component legs are fully inserted into the breadboard.

---

# 14. Wiring Checklist

Before powering your circuit:

* [ ] Arduino GND is connected to circuit GND
* [ ] Components are connected to the correct pins
* [ ] LEDs have resistors
* [ ] Polarity-sensitive components are oriented correctly
* [ ] Power connections are correct
* [ ] No wires are accidentally shorting 5V to GND
* [ ] Code uses the same pins as the physical circuit

---

# 15. The Most Important Rule

**Always understand where electricity is flowing.**

Before powering your circuit, trace the path:

```text
Power → Component → Ground
```

For example:

```text
Arduino Pin 13
      ↓
   Resistor
      ↓
     LED
      ↓
    Ground
```

If you can trace the path through your circuit, you are much more likely to find wiring problems.

Once your circuit is wired correctly, connect your Arduino, upload your code, and start experimenting!
