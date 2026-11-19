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

By completing this project, students will learn how software and electronics can work together to control a physical mechanism.

**Happy building! 🔧**
