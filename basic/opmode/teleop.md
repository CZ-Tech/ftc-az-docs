# teleop: the code of manual phase

## abstract

Route:

> opmode/teleop

After asking our operator, we found that key press, release, keep pressing and toggle are more commonly used, so we encapsulated **keyPress**, **keyDown**, **keyUp** and **keyToggle** to simplify the detection of gamepad buttons and implement chains to make the code more concise and understandable.

## introduction
### Parameter list
- key: Keys to detect, whose name is the same as the handle key name in ```FTC SDK```, and it is defined as ```String```type.
- fn: Metods to run. It is recommended to use **Lambda expression**, and it is defined as ```Runnnable``` type.

### Defining gamepad

```java
robot.gamepad1
    .update()//Update the state
    .keyPress("a",Runnable)//Press a to run the runnable method
    .keyUp("b",Runnable)//Release b to run the runnable method
    .keyDown("x",Runnable)//Keep pressing x to keep the runnable method running
    .keyToggle("y",Runnable1, Runnable2)//Press y to switch
;
```
Define the buttons on the gamepad. Details can be found in [gamepadEX](basic/gamepadex.md).

### Field coordinate system

We use ```robot.drivetrain.driveRobotFieldCentric()```method to help find direction in coordinate system based on the field. However, in practice, the operator may not know the direction of the machine for various reasons, so it is necessary to define a new button to reset the field coordinates.

```java
robot.drivetrain.driveRobotFieldCentric(
        gamepad1.left_stick_y,
        gamepad1.left_stick_x,
        gamepad1.right_stick_x
);
```
If you are not used to field coordinate system, you can use ```robot.drivetrain.driveRobot()```method to make robot itself the origin of coordinate system.

```java
robot.drivetrain.driveRobot(
        gamepad1.left_stick_y,
        gamepad1.left_stick_x,
        gamepad1.right_stick_x
);
```
**Which method is chosen depends on the operator**

### Gamepad stick curve
If your operator feel bad on the gamepad. You can change or delete the method, which doesn't cause any problem to your code.
```java
private double sss(double v) {
    if (v > 0.0) {//If there is drift in the proccess of driving, change the value to 0.01.
        v = 0.87 * v * v * v + 0.09;//0.09 is the power that is needed to drive the robot in season 24-25.
    } else if (v < 0.0) { //If there is drift in the proccess of driving, change the value to -0.01
        v = 0.87 * v * v * v - 0.09; 
    } else {
        //If there is drift in the proccess of driving, change the value of v to 9
        //This 9 is from 0.09/0.01=9
        v = 0;
    }
    return v;
}
```
