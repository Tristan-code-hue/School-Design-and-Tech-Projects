# 🔐 Arduino Secret Box Project

## About This Project

In this project, you will learn how to create a **password-protected locking system** using an Arduino Uno, three buttons, and a servo motor.

The goal is to build a system where you must press three buttons in the correct order to unlock a box.

For now, this project will be completed entirely in **Tinkercad Circuits**, so you don't need a physical Arduino or any electronic components.

**Difficulty:** Beginner–Intermediate  
**Estimated circuit setup time:** 30–60 minutes  
**Programming language:** Arduino C++  
**Software:** [Tinkercad Circuits](https://www.tinkercad.com/)

---

## 1. Materials Needed

All of these components are available virtually in Tinkercad.

| Component | Quantity | Purpose |
|---|---|---|
| Arduino Uno R3 | 1 | Controls the system |
| Breadboard | 1 | Connects components |
| Pushbuttons | 3 | Enter the password |
| Micro servo motor | 1 | Operates the lock |
| Jumper wires | As needed | Connects everything |

### What Do These Components Do?

**Arduino Uno:** A small programmable computer that controls electronic components.

**Breadboard:** A board that allows you to connect electronic components without soldering.

**Pushbutton:** A switch that sends a signal when pressed.

**Servo Motor:** A motor that can rotate to a specific angle. We will use it to simulate locking and unlocking a box.

---

## 2. Wiring Instructions

Open [Tinkercad](https://www.tinkercad.com/) and create a new circuit.

Add the components listed above.

### Connecting the Buttons

Each button will be connected to an Arduino digital pin and GND (ground).

| Button | Arduino Pin | Other Connection |
|---|---|---|
| Red Button | 2 | GND |
| Blue Button | 3 | GND |
| Green Button | 4 | GND |

**Important:** On a typical four-legged pushbutton, the two legs on the same side are already electrically connected.

Connect your wires to opposite sides of the switch so pressing the button completes the circuit.

We will use the Arduino's built-in pull-up resistors, so **no additional resistors are needed for the buttons**.

### Connecting the Servo Motor

A servo motor has three wires.

| Servo Wire | Arduino Connection |
|---|---|
| Red (Power) | 5V |
| Brown/Black (Ground) | GND |
| Orange/Yellow (Signal) | Digital Pin 9 |

The signal wire tells the servo what angle to rotate to.

**Note:** This wiring is for the Tinkercad simulation. A physical servo may require a separate regulated 5V power supply.

---

## 3. Arduino Code

Click **Code** in Tinkercad and change the programming mode to **Text**.

Delete the existing code and paste the following:

```cpp
#include <Servo.h>

Servo lockServo;

const int redButton = 2;
const int blueButton = 3;
const int greenButton = 4;

const int servoPin = 9;

// Correct password: Red, Blue, Green
const int password[] = {0, 1, 2};

int position = 0;
bool unlocked = false;

void setup() {
  pinMode(redButton, INPUT_PULLUP);
  pinMode(blueButton, INPUT_PULLUP);
  pinMode(greenButton, INPUT_PULLUP);

  lockServo.attach(servoPin);
  lockServo.write(0); // Locked
}

void loop() {
  if (unlocked) return;

  int pressed = -1;

  if (digitalRead(redButton) == LOW) {
    pressed = 0;
  } else if (digitalRead(blueButton) == LOW) {
    pressed = 1;
  } else if (digitalRead(greenButton) == LOW) {
    pressed = 2;
  }

  if (pressed != -1) {
    if (pressed == password[position]) {
      position++;

      if (position == 3) {
        lockServo.write(90);
        unlocked = true;
      }
    } else {
      position = 0;
    }

    // Wait until all buttons are released
    while (digitalRead(redButton) == LOW ||
           digitalRead(blueButton) == LOW ||
           digitalRead(greenButton) == LOW) {
      delay(10);
    }

    delay(50); // Debounce
  }
}
```

---

## 4. Understanding the Code

Don't worry if you've never programmed an Arduino before!

Let's explain the important parts.

### Part 1: Servo Library

```cpp
#include <Servo.h>
Servo lockServo;
```

The Servo library allows the Arduino to control a servo motor.

`lockServo` is the name we give our servo in the program.

### Part 2: Choosing the Pins

```cpp
const int redButton = 2;
const int blueButton = 3;
const int greenButton = 4;

const int servoPin = 9;
```

These lines tell the Arduino where everything is connected.

### Part 3: Setting the Password

```cpp
const int password[] = {0, 1, 2};
```

Each number represents a button:

- `0` = Red
- `1` = Blue
- `2` = Green

Our password is:

**Red → Blue → Green**

The order matters!

### Part 4: Setting Up the Buttons

```cpp
pinMode(redButton, INPUT_PULLUP);
pinMode(blueButton, INPUT_PULLUP);
pinMode(greenButton, INPUT_PULLUP);
```

`INPUT_PULLUP` activates the Arduino's built-in pull-up resistors.

This means:

- `HIGH` = Button not pressed
- `LOW` = Button pressed

### Part 5: Locking and Unlocking

```cpp
lockServo.write(0);
```

Moves the servo to 0 degrees, our simulated locked position.

```cpp
lockServo.write(90);
```

Moves the servo to 90 degrees, our simulated unlocked position.

When the correct password is entered, the servo rotates to 90 degrees and stays there.

### Part 6: Checking the Password

```cpp
if (pressed == password[position]) {
  position++;
}
```

This checks whether the button pressed matches the next button in the password.

If the wrong button is pressed, the program resets the password progress.

---

## 5. Running the Simulation

### Step 1: Open Tinkercad

1. Go to [Tinkercad](https://www.tinkercad.com/).
2. Sign in using the method provided by your teacher.
3. Open **Circuits**.
4. Click **Create New Circuit**.

### Step 2: Build Your Circuit

1. Add an Arduino Uno R3.
2. Add a breadboard.
3. Add three pushbuttons.
4. Add a micro servo.
5. Connect everything according to Section 2.

### Step 3: Upload the Code Virtually

1. Click **Code**.
2. Select **Text** mode.
3. Paste the code from Section 3.
4. Click **Start Simulation**.

### Step 4: Test the Password

Press the buttons in this order:

**Red → Blue → Green**

If everything works, the servo should rotate from 0° to 90°.

Try pressing the buttons in the wrong order.

The servo should stay locked.

**Congratulations! You have created a working Arduino password lock!**

---

## 6. Troubleshooting

### The Servo Doesn't Move

Check that:

- The signal wire is connected to pin 9.
- The power wire is connected to 5V.
- The ground wire is connected to GND.
- The simulation is running.
- The correct password is being entered.

### The Buttons Don't Work

- Make sure the buttons are connected to pins 2, 3, and 4.
- Check that each button connects to GND when pressed.
- Make sure you are using opposite switch contacts.
- Check that the buttons are placed correctly on the breadboard.

### The Servo Unlocks With the Wrong Password

- Double-check the button connections.
- Make sure the code matches the wiring.
- Restart the simulation and try again.

### The Servo Won't Lock Again

This is normal!

Our current program is designed to remain unlocked after the correct password is entered.

To lock it again, stop and restart the simulation.

---

## 7. Experimenting With the Project

Once your circuit works, try these challenges.

### Beginner Challenges

- Change the password to a different button sequence.
- Change the servo's unlocked angle.
- Add a fourth button.

### Intermediate Challenges

- Add a green LED that turns on when the box unlocks.
- Add a red LED that indicates the box is locked.
- Make the servo automatically lock again after a few seconds.

### Advanced Challenges

- Create a longer password.
- Add a buzzer for incorrect passwords.
- Design a 3D-printed box and locking mechanism.

---

## 8. Turning the Circuit Into a Secret Box

The circuit is only the first part of the project.

Eventually, students could design and 3D-print a small box with a locking mechanism.

The servo would move a latch when the correct password is entered.

For the classroom version, the Arduino, servo, and buttons would remain at school.

Students could take home their 3D-printed boxes with a separate manual sliding latch.

This allows students to keep their projects without needing to purchase an Arduino.

---

## 9. Classroom Feasibility Testing

This project is being tested to determine whether it is suitable for a Design and Tech class.

### Things to Evaluate

- [ ] Can beginners understand the wiring?
- [ ] Can students assemble the circuit without major assistance?
- [ ] Does the code work reliably in Tinkercad?
- [ ] Can students understand how the password works?
- [ ] Can a simple box and latch be 3D-printed?
- [ ] Can the project be completed within a reasonable number of class periods?

### Initial Time Estimates

| Activity | Estimated Time |
|---|---|
| Learning the components | 10–15 minutes |
| Building the circuit | 20–35 minutes |
| Adding and testing code | 15–25 minutes |
| Troubleshooting | 10–20 minutes |
| Designing a simple box | 45–90 minutes |
| Assembling the box | 20–40 minutes |

**Estimated total:** Approximately 2–4 class periods, depending on experience, the provided design, and class length. 3D-printing time is additional.

These are planning estimates, not measured classroom results.

### Prototype Status

- [x] Basic Arduino circuit simulated successfully
- [x] Password sequence tested successfully
- [x] Servo unlocking tested successfully
- [ ] 3D-printed box designed
- [ ] Physical locking mechanism tested
- [ ] Full classroom feasibility confirmed

---

## Project Goal

The goal of this project is to introduce students to Arduino programming, servo motors, buttons, and basic mechanical engineering.

---

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
