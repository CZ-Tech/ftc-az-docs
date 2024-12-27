# GamepadEX: gamepad extension

## Abstract

### Route
> drive/Drivetrain

After asking the operators, we found that button press, release, keep pressing and toggle were  commonly used. As a result we encapsulated methods like **keyPress**, **keyDown**, **keyUp** and **keyToggle**, which simplified the detection of handle buttons and introduced chains to make the code more simple and understandable.

## Details

### Parameter list

- ```key```: Keys to detect. It should be consistent with the handle button names in the ```FTC SDK```.  It is the ```String``` class.
- ```Runnable```: Method to be executed.  It is recommended to use **Lambda**,It is ``Runnnable`` class.

### Update

Every time you define the gamepad keystroke, you need to run it once first and use it to update the gamepad state. Otherwise each loop will use the last state and will not be able to determine the state of the keys.

**Example:**

```java
robot.gamepad1
    .update()
    .<other methods>
;
```

### KeyPress
When key is pressed, ```Runnable``` is executed. Note: ```Runnable``` runs **in a loop** for the duration of the ``key`` being pressed.

**Example:**

```java
robot.gamepad1
    .update()
    .keyPress("a",Runnable)//press a
;
```

### KeyDown
When key is pressed, ```Runnable``` is executed. Note: ```Runnable``` runs **once** the moment the key is pressed.

**Example:**

```java
robot.gamepad1
    .update()
    .keyDown("a",Runnable)//tap a
;
```

### KeyUp

When key is pressed, ```Runnable``` is executed. Note: ```Runnable``` runs **once** the moment the key is released.

**Example:**

```java
robot.gamepad1
    .update()
    .keyUp("a",Runnable)//release a
;
```

### KeyToggle

When key is pressed, ```Runnable1``` are executed once; when ```key``` is pressed again,```Runnable2``` are executed once, and so on.

**Example:**

```java
robot.gamepad1
    .update()
    .keyToggle("a",Runnable1, Runnable2)//tap a to run different runnable
;
```

**It is recommended that telemetry information be added to the switching function to confirm the current state**.