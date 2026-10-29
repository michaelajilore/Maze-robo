# Arduino Programming Basics

A hands-on beginner course using virtual circuits, code, and experiments in [Wokwi](https://wokwi.com) with an Arduino Uno.

**Teach • Build • Test • Debug**

> **Copying code:** hover over any code block and click the copy icon in its top-right corner, then paste it into `sketch.ino` in Wokwi. Every code block is a complete sketch except the capstone starter code, which has blanks for you to fill in.

## Contents

1. [What you'll learn](#what-youll-learn)
2. [Set up your Wokwi workspace](#set-up-your-wokwi-workspace)
3. [Lesson 1: Program structure](#lesson-1-program-structure)
4. [Lesson 2: Digital outputs](#lesson-2-digital-outputs)
5. [Lesson 3: Variables](#lesson-3-variables)
6. [Lesson 4: Make decisions](#lesson-4-make-decisions)
7. [Lesson 5: Digital inputs](#lesson-5-digital-inputs)
8. [Lesson 6: Loops and functions](#lesson-6-loops-and-functions)
9. [Lesson 7: Debugging](#lesson-7-debugging)
10. [Capstone: Traffic light controller](#capstone-traffic-light-controller)
11. [Review: What can you build now?](#review-what-can-you-build-now)

---

## What you'll learn

- Understand the structure of an Arduino sketch.
- Control LEDs with digital output pins.
- Use variables and timing to change behavior.
- Make decisions with `if` / `else` conditions.
- Read buttons and respond to user input.
- Use loops, functions, and Serial Monitor debugging.
- Build a traffic-light controller in Wokwi.

---

## Set up your Wokwi workspace

1. **Open:** go to [wokwi.com](https://wokwi.com) and create a new Arduino Uno project.
2. **Code:** write your program in `sketch.ino`.
3. **Build:** add components and connect wires in the diagram editor.
4. **Run:** click Play to start the simulation.
5. **Observe:** use the circuit and Serial Monitor to check behavior.
6. **Save:** save each project and explain what your code does.

> Use an Arduino Uno for all lessons unless an exercise says otherwise.

---

## Lesson 1: Program structure

### Anatomy of an Arduino sketch

```cpp
void setup() {
  // Runs once at startup
}

void loop() {
  // Repeats continuously
}
```

**What to notice**

- `setup()` runs once when the Arduino starts or resets.
- `loop()` repeats for as long as the program runs.
- `{ }` group statements into a code block.
- `//` begins a single-line comment.
- Most statements end with a semicolon (`;`).

### Your first program

```cpp
void setup() {
  Serial.begin(9600);
  Serial.println("Hello, Arduino!");
}

void loop() {
}
```

**In Wokwi:**

1. Open the Serial Monitor.
2. Start the simulation.
3. Confirm the message appears.

**What to notice**

- `Serial.begin(9600)` starts serial communication.
- `println()` prints text and starts a new line.

### Practice: Program structure

1. Replace the greeting with your name.
2. Print your name, hobby, and "Ready!" on separate lines.
3. Move `Serial.println("Running!")` into `loop()`. What changes?
4. Fix the missing semicolon and incorrect capitalization.

**Challenge:** explain why the loop version prints repeatedly.

---

## Lesson 2: Digital outputs

### Control an LED

```cpp
int ledPin = 13;

void setup() {
  pinMode(ledPin, OUTPUT);
  digitalWrite(ledPin, HIGH);
}

void loop() {
}
```

**What to notice**

- `pinMode()` configures a pin.
- `OUTPUT` means the pin sends a signal.
- `HIGH` turns the LED on in this circuit. `LOW` turns it off.

> You can use the built-in LED on pin 13 or add an external LED.

### Make it blink: timing with `delay()`

```cpp
int ledPin = 13;

void setup() {
  pinMode(ledPin, OUTPUT);
}

void loop() {
  digitalWrite(ledPin, HIGH);
  delay(1000);

  digitalWrite(ledPin, LOW);
  delay(1000);
}
```

**What to notice**

- `delay(1000)` pauses for about 1,000 milliseconds (1 second).
- The loop repeats: ON for 1 second → OFF for 1 second.

> **External LED:** use a 220 Ω resistor and connect the cathode to GND.

### Practice: Digital outputs

1. Blink faster: 250 ms on, 250 ms off.
2. Blink slowly: 3 seconds on, 1 second off.
3. Add a second LED on pin 12; alternate the LEDs.
4. Make three short flashes, then three long flashes.
5. Debug an LED that never lights up.

> Check pin numbers, `OUTPUT` mode, LED orientation, resistor, and GND.

---

## Lesson 3: Variables

### Store values

```cpp
int ledPin = 13;
int waitTime = 500;

void setup() {
  pinMode(ledPin, OUTPUT);
}

void loop() {
  digitalWrite(ledPin, HIGH);
  delay(waitTime);
  digitalWrite(ledPin, LOW);
  delay(waitTime);
}
```

**What to notice**

- A variable stores a value the program can reuse.
- `int` stores whole numbers.
- `ledPin` stores the pin number.
- `waitTime` stores milliseconds.

> Change `waitTime` to 100 or 1500 and observe the speed.

### Count with a variable

```cpp
int counter = 0;

void setup() {
  Serial.begin(9600);
}

void loop() {
  counter = counter + 1;
  Serial.println(counter);
  delay(1000);
}
```

**What to notice**

- `counter` starts at zero.
- Each loop adds one.
- The updated value is printed every second.

> `counter++` is shorthand for adding one.

### Practice: Variables and timing

1. Test LED `waitTime` values of 100, 500, and 1500.
2. Print a counter once every 2 seconds.
3. Count down from 10 to 0, then restart.
4. Use variables for two LED pins and their delay times.

> Explain which values are stored and where each variable is used.

---

## Lesson 4: Make decisions

### If / else

```cpp
int temperature = 30;

void setup() {
  Serial.begin(9600);

  if (temperature > 25) {
    Serial.println("It is warm.");
  } else {
    Serial.println("It is not warm.");
  }
}

void loop() {
}
```

**What to notice**

- The condition is checked once in `setup()`.
- If `temperature > 25` is true, the first block runs.
- Otherwise, the `else` block runs.

> **Remember:** `=` assigns; `==` compares.

### Comparison and logic operators

| Operator | Meaning |
| --- | --- |
| `==` | Equal to |
| `!=` | Not equal to |
| `>` / `<` | Greater than / less than |
| `>=` / `<=` | Greater than or equal / less than or equal |
| `&&` | Logical AND: both conditions must be true |
| `\|\|` | Logical OR: at least one condition must be true |

> Try changing the values in Wokwi and predict which branch will run.

### Practice: Decisions and logic

1. Print Positive, Negative, or Zero.
2. Print Pass if a score is at least 70; otherwise Fail.
3. Turn an LED on at counter 10 and off at 15; repeat.
4. Print Valid only when a number is greater than 0 and less than 100.
5. Use a state variable to control red, yellow, and green LEDs.

---

## Lesson 5: Digital inputs

### Read a pushbutton

```cpp
int buttonPin = 2;
int ledPin = 13;

void setup() {
  pinMode(buttonPin, INPUT_PULLUP);
  pinMode(ledPin, OUTPUT);
}

void loop() {
  int buttonState = digitalRead(buttonPin);

  if (buttonState == LOW) {
    digitalWrite(ledPin, HIGH);
  } else {
    digitalWrite(ledPin, LOW);
  }
}
```

**Wiring**

- Connect button pin `1.l` or `1.r` to Arduino pin **2**.
- Connect button pin `2.l` or `2.r` to **GND**.

> In Wokwi, `1.l` and `1.r` are always connected to each other (as are `2.l` and `2.r`). The "2" in the button's pin names is its second contact, not Arduino pin 2.

**What to notice**

- `INPUT_PULLUP` means: `LOW` = pressed, `HIGH` = released.
- The LED follows the button while it is held.

### Practice: Inputs

1. Make the LED turn on only while the button is held.
2. Reverse the behavior.
3. Print a message while the button is pressed; observe repeated output.
4. Add a second button on pin 3: one turns the LED on, one turns it off.

> A held button is a **state**; a new press is an **event**.

---

## Lesson 6: Loops and functions

### Repeat with a `for` loop

```cpp
void setup() {
  Serial.begin(9600);

  for (int i = 1; i <= 5; i++) {
    Serial.println(i);
  }
}

void loop() {
}
```

**What to notice**

A `for` loop has three parts:

1. Initialize: `int i = 1`
2. Continue while: `i <= 5`
3. Update: `i++`

> This loop runs once during `setup()`.

### Reuse code with functions

```cpp
int ledPin = 13;

void blinkLED() {
  digitalWrite(ledPin, HIGH);
  delay(500);
  digitalWrite(ledPin, LOW);
  delay(500);
}

void setup() {
  pinMode(ledPin, OUTPUT);
}

void loop() {
  blinkLED();
}
```

**What to notice**

- `blinkLED()` groups reusable instructions.
- Calling `blinkLED()` runs the function.
- Because `loop()` repeats, the function is called repeatedly.

> Functions reduce duplicated code.

### Practice: Loops and functions

1. Print even numbers from 2 through 20.
2. Count down from 10 to 1, then print "Launch!".
3. Write a function that blinks an LED three times.
4. Create `turnOn()` and `turnOff()` functions for two LEDs.

---

## Lesson 7: Debugging

### Debugging checklist: find the problem systematically

| Check | What to look for |
| --- | --- |
| **Syntax** | Missing semicolons, braces, or misspelled function names. |
| **Pins** | Does the code pin number match the circuit? |
| **Circuit** | Check LED direction, resistor, and GND. |
| **Inputs** | Check `INPUT_PULLUP` logic and button wiring. |
| **Serial** | Confirm `Serial.begin()` and that the print statement runs. |
| **Program flow** | Check `setup()`, `loop()`, conditions, and variable resets. |

> Change one thing at a time, run the simulation, and observe the result.

### Practice: Debug the program

1. Fix a missing semicolon.
2. Fix a pin mismatch: code uses 12 but LED is wired to 13.
3. Investigate why a counter restarts at zero.
4. Print a button state to diagnose an always-on LED.

> Explain both the bug and why your fix works.

---

## Capstone: Traffic light controller

### The project

| Stage | Pin | Time on |
| --- | --- | --- |
| Red | 13 | 3 seconds |
| Green | 11 | 3 seconds |
| Yellow | 12 | 1 second |
| Repeat | | Keep cycling through the sequence. |

**Circuit:** use one LED and 220 Ω resistor per color; connect cathodes to GND.

> Only the intended LED should be on during each stage.

### Starter code: complete the timing

Fill in each `____` with a delay in milliseconds. The sketch won't compile until all three blanks are filled.

- Red: 3 seconds
- Green: 3 seconds
- Yellow: 1 second

> **Hint:** 1 second = 1,000 milliseconds.

```cpp
int redLED = 13;
int yellowLED = 12;
int greenLED = 11;

void setup() {
  pinMode(redLED, OUTPUT);
  pinMode(yellowLED, OUTPUT);
  pinMode(greenLED, OUTPUT);
}

void loop() {
  // Red stage
  digitalWrite(redLED, HIGH);
  digitalWrite(yellowLED, LOW);
  digitalWrite(greenLED, LOW);
  delay(____);

  // Green stage
  digitalWrite(redLED, LOW);
  digitalWrite(yellowLED, LOW);
  digitalWrite(greenLED, HIGH);
  delay(____);

  // Yellow stage
  digitalWrite(redLED, LOW);
  digitalWrite(yellowLED, HIGH);
  digitalWrite(greenLED, LOW);
  delay(____);
}
```

### Extension challenges

1. Print a countdown for each light stage.
2. Add a pedestrian button and a safe crossing sequence.
3. Refactor the code into `setRed()`, `setYellow()`, and `setGreen()`.
4. Replace `delay()` with `millis()` so buttons can be checked while timing.

> This is a learning simulation, not a certified real-world traffic controller.

---

## Review: What can you build now?

- [ ] Describe the roles of `setup()` and `loop()`.
- [ ] Configure a pin and control an LED.
- [ ] Use variables to make code easier to change.
- [ ] Use `if` / `else` to make decisions.
- [ ] Read a button and interpret its state.
- [ ] Use loops and functions to simplify code.
- [ ] Debug a circuit using systematic checks and Serial Monitor output.

**Next step:** design a small Wokwi project of your own.
