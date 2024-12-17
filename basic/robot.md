# Robot:the origin of all

## Abstract

```Robot.java``` contains all robot modules and is used as a unified entry point for the code. This makes it possible to rewrite repetitive code into function calls and be more readable.
### trails

> common\Robot.java
## introduction
### initialization
In either manual or automatic code, the **Robot** object needs to be defined first:
```java
Robot robot = new Robot();
```
Then,use ```robot.init(this)```in```runOpMode()``` to initialize the Robot object:

```java
@Override
public void runOpMode() {
    robot.init(this);
    /*Main Methods*/
}
```
### Usage
As a unified entry point for the code,all controlling over the robot can be invoked from```robot.\<module>.\<method>```And part of the code supports chains, examples are as follows:

```java
robot.drivetrain.driveStrafe(-65.0, 0, DRIVESPEED);//drivetrain module
robot.subsystem.slamDunker.grab();//subsystem invocation
robot.gamepad1.update();//gamepadex Module
/*Other Methods*/
```
### Detials
```Robot.java```Contains all the module entries for the machine, some of the commonly used modules are described below:
#### HardwareMap
Get the hardware via the hardware name edited on Driver Hub.
#### Telemetry
Telemetry on the Driver Hub for displaying information.
#### drivetrain
For chassis movement, see: [drivetrain](drivetrain.md)
#### subsystem
The subsystem of robot, including the control of arms.
#### gamepad
Operations of gamepadex, see:[gamepadex](gamepadex.md)
