# Arduino IDE Installation Guide

Before you can program an Arduino, you need to install the **Arduino IDE** on your computer.

The Arduino IDE is the software used to write, compile, and upload code to your Arduino.

---

## 1. Download Arduino IDE

Go to the official Arduino website:

[Arduino IDE Download](https://www.arduino.cc/en/software/)

Download the version for your operating system:

* **Windows**
* **macOS**
* **Linux**

---

## 2. Install Arduino IDE

### Windows

1. Download the **Windows** installer.
2. Open the downloaded installer.
3. Follow the installation instructions.
4. Allow the installer to install any required drivers.
5. Open **Arduino IDE** when the installation is complete.

### macOS

1. Download the **macOS** version.
2. Open the downloaded file.
3. Drag **Arduino IDE** into your Applications folder.
4. Open Arduino IDE from Applications.
5. If macOS asks for permission to open the application, allow it.

### Linux

1. Download the appropriate Linux version.
2. Extract the downloaded file.
3. Follow the installation instructions provided by Arduino.
4. Open Arduino IDE.

---

# 3. Connect Your Arduino

Connect your Arduino to your computer using a USB cable.

> **Important:** Make sure your USB cable supports **data transfer**. Some USB cables are designed only for charging.

Once connected, your Arduino should receive power and the power LED should turn on.

---

# 4. Select Your Board

Open Arduino IDE.

Go to:

**Tools → Board**

Select the Arduino board you are using.

For example:

```text
Tools
  └── Board
       └── Arduino AVR Boards
            └── Arduino Uno
```

If you are using a different Arduino board, select the appropriate board.

---

# 5. Select the Port

Connect your Arduino to your computer and open:

**Tools → Port**

Select the port associated with your Arduino.

It may look something like:

```text
COM3
COM4
COM5
```

On macOS, it may look similar to:

```text
/dev/cu.usbmodem...
```

If you are unsure which port is your Arduino, disconnect the Arduino, check the available ports, reconnect it, and see which port appears.

---

# 6. Test Your Arduino

Let's test that everything is working.

Open:

**File → Examples → 01.Basics → Blink**

You should see code similar to:

```cpp
void setup() {
  pinMode(LED_BUILTIN, OUTPUT);
}

void loop() {
  digitalWrite(LED_BUILTIN, HIGH);
  delay(1000);

  digitalWrite(LED_BUILTIN, LOW);
  delay(1000);
}
```

Click the **Upload** button.

The upload button looks like an arrow pointing to the right:

```text
→
```

Wait for the upload to finish.

If everything worked correctly, the built-in LED on your Arduino should blink once every second.

---

# 7. Writing Your Own Code

Once your Arduino is working, you can create a new sketch.

Go to:

**File → New Sketch**

A basic Arduino program looks like this:

```cpp
void setup() {

}

void loop() {

}
```

Put code that should run **once** inside `setup()`.

Put code that should run **repeatedly** inside `loop()`.

For example:

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

---

# 8. Uploading Your Code

Whenever you want to run your code on the Arduino:

1. Connect the Arduino to your computer.
2. Select the correct board.
3. Select the correct port.
4. Click **Verify** to check the code.
5. Click **Upload**.
6. Wait for the upload to finish.
7. Test your circuit.

### Verify

The **Verify** button checks your code for errors without uploading it.

### Upload

The **Upload** button compiles your code and sends it to the Arduino.

---

# 9. Troubleshooting

## Arduino does not appear under Ports

Try:

* Disconnecting and reconnecting the Arduino.
* Trying a different USB cable.
* Trying a different USB port.
* Restarting Arduino IDE.
* Checking whether the correct drivers are installed.

## Code will not upload

Check:

* The correct board is selected.
* The correct port is selected.
* The Arduino is connected.
* No other program is using the Arduino's serial port.

## Code has an error

Check:

* Spelling
* Semicolons `;`
* Parentheses `()`
* Curly brackets `{ }`
* Variable names
* Missing libraries

---

# Quick Start Checklist

Before starting a project, make sure:

* [ ] Arduino IDE is installed
* [ ] Arduino is connected
* [ ] Correct board is selected
* [ ] Correct port is selected
* [ ] Code has been verified
* [ ] Code has been uploaded
* [ ] Circuit is wired correctly

Once everything is working, you're ready to start building!
