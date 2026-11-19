
# Arduino Glowing Name Plate 

## About This Project

This project teaches you how to use an **Arduino Uno** to control three LEDs (red, green, and blue).

When the program runs, all three LEDs turn on and stay on. This can be used to illuminate a 3D-printed name plate!

**Difficulty:** Beginner  
**Estimated setup time:** 15–30 minutes  
**Programming language:** Arduino C++

## 1. Materials Needed

Before starting, gather these materials:

- 1 Arduino Uno
- 1 breadboard
- 3 LEDs (red, green, and blue)
- 3 resistors (220 ohms each)
- Jumper wires
- USB cable for the Arduino
- A computer with Arduino IDE or access to Tinkercad Circuits

**What is a breadboard?**

A breadboard lets you connect electronic components without soldering. The holes are connected internally in groups, allowing electricity to travel between components.

## 2. Circuit Diagram

Follow this picture to connect everything:

<img width="572" height="467" alt="Arduino Uno glowing name plate LED wiring diagram" src="https://github.com/user-attachments/assets/bc06ac0b-4a02-43d1-a3ae-9a7f74d2b314" />

### Wiring Instructions

Connect the LEDs to these Arduino pins:

| LED Color | Arduino Pin | Resistor |
|---|---|---|
| Red | 9 | 220 Ω |
| Green | 8 | 220 Ω |
| Blue | 7 | 220 Ω |

Each LED has two legs:

- **Anode (+):** The positive leg, usually the longer one.
- **Cathode (−):** The negative leg, usually the shorter one.

For each LED, connect:

1. The Arduino digital pin to the LED's anode (+).
2. The LED's cathode (−) to one end of a 220 Ω resistor.
3. The other end of the resistor to GND (ground).

**Important:** Every LED needs its own resistor to limit the electrical current and help prevent damage.

## 3. Arduino Code

Copy the following code into Arduino IDE or Tinkercad's text editor.

```cpp
const int redLED = 9;
const int greenLED = 8;
const int blueLED = 7;

void setup() {
  pinMode(redLED, OUTPUT);
  pinMode(greenLED, OUTPUT);
  pinMode(blueLED, OUTPUT);
}

void loop() {
  digitalWrite(redLED, HIGH);
 

  digitalWrite(greenLED, HIGH);
 
  digitalWrite(blueLED, HIGH);
}
```

## 4. Understanding the Code

You don't need any programming experience to understand the basics!

### Part 1: Choosing the Pins

```cpp
const int redLED = 9;
const int greenLED = 8;
const int blueLED = 7;
```

These lines tell the Arduino which pins are connected to each LED.

For example, `redLED = 9` means the red LED is connected to digital pin 9.

### Part 2: Setting Up the Arduino

```cpp
void setup() {
  pinMode(redLED, OUTPUT);
  pinMode(greenLED, OUTPUT);
  pinMode(blueLED, OUTPUT);
}
```

The `setup()` function runs once when the Arduino starts.

`OUTPUT` tells the Arduino that these pins will send electrical signals to the LEDs.

### Part 3: Turning On the LEDs

```cpp
void loop() {
  digitalWrite(redLED, HIGH);
  digitalWrite(greenLED, HIGH);
  digitalWrite(blueLED, HIGH);
}
```

The `loop()` function repeats continuously.

`digitalWrite()` controls whether a pin is on or off.

- `HIGH` = Turn the pin on.
- `LOW` = Turn the pin off.

Since all three LEDs are set to `HIGH`, they stay illuminated.


## 5. Running the Project in Tinkercad

For this project, we will use **Tinkercad Circuits** to build, program, and test our Arduino circuits virtually.

You do not need a physical Arduino or any electronic components.

### Step 1: Open Tinkercad

1. Go to [Tinkercad](https://www.tinkercad.com/).
2. Sign in using the method provided by your teacher.
3. Open the **Circuits** section.
4. Click **Create New Circuit**.

### Step 2: Add Your Components

Find and add the following components:

- 1 Arduino Uno R3
- 1 breadboard
- 3 LEDs (red, green, and blue)
- 3 resistors (220 Ω each)
- Jumper wires

### Step 3: Connect Everything

Follow the circuit diagram in Section 2.

Make sure:

- Red LED connects to pin 9.
- Green LED connects to pin 8.
- Blue LED connects to pin 7.
- Each LED has its own 220 Ω resistor.
- All three LED circuits connect to GND.

### Step 4: Add the Code

1. Click **Code** in the upper-right corner.
2. Switch the programming mode to **Text**.
3. Delete the existing code.
4. Copy and paste the Arduino code from Section 3.

### Step 5: Start the Simulation

1. Click **Start Simulation**.
2. Watch your LEDs.
3. All three LEDs should turn on and stay illuminated.

**Congratulations!** You have successfully built your first Arduino LED circuit!

### Step 6: Experiment

Once your circuit works, try making changes:

- Change the LED colors.
- Add another LED with its own resistor.
- Make an LED blink using `delay()`.
- Experiment with different lighting patterns.

**Remember:** If you add more LEDs, make sure the Arduino's pins aren't overloaded.

---

### Classroom Notes

This project is currently designed for **Tinkercad simulation only**. Physical Arduino construction may be introduced later.

The goal is to understand basic circuits and Arduino programming before working with real electronic components.
## 6. Troubleshooting

**Problem: An LED doesn't turn on.**

Check that:

- The LED is facing the correct direction.
- The wires are connected to the correct Arduino pins.
- The resistor is connected properly.
- The LED's circuit has a connection to GND.

**Problem: The code won't upload.**

- Make sure the Arduino is connected to the computer.
- Check that you selected Arduino Uno.
- Make sure you selected the correct USB port.
- Try another USB cable if the computer doesn't recognize the Arduino.

**Problem: The simulation starts, but nothing happens.**

- Check that your code uses pins 9, 8, and 7.
- Verify the breadboard connections.
- Make sure the LEDs aren't connected backward.

## 7. Next Steps

Once the basic circuit works, try experimenting!

- Add more LEDs to illuminate a larger name plate.
- Change the code to make the LEDs blink.
- Create different lighting patterns.
- Design a name plate using Tinkercad's 3D modeling tools.
- Experiment with a battery-powered version that doesn't need an Arduino.

**Note:** When adding more LEDs, make sure you stay within the Arduino's electrical current limits. Larger groups of LEDs may require a separate power supply and transistor drivers.

---

## Project Goal

The goal of this project is to learn basic electronics, Arduino programming, and circuit design while creating something that can eventually become a glowing 3D-printed name plate.

**Happy building!** 🔧
