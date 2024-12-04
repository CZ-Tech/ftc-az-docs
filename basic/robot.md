# Robot:the origin of all

## Abstract

**Robot.java** contains all robot modules and is used as a unified entry point for the code. This makes it possible to rewrite repetitive code into function calls and be more readable.
### trails

> common\Robot.java
## presentation
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
As a unified entry point for the code,all controlling over the robot can be invoked from```robot.\<module>.\<method>```And part of the code supports chaining, examples are as follows:

```java
robot.drivetrain.driveStrafe(-65.0, 0, DRIVESPEED);//mobile module
robot.subsystem.slamDunker.grab();//subsystem invocation
robot.gamepad1.update();//Handle Module
/*Other Methods*/
```
### 详细解释
**Robot.java**Contains all the module entries for the machine, some of the commonly used modules are described below:
#### hardwareMap
Get the hardware via the hardware name edited on Driver Hub.
#### telemetry
Driver Hub上的遥测，用于显示信息。
#### drivetrain
用于机器底层移动，详见[drivetrain](drivetrain.md)
#### subsystem
机器的子系统，包含上层的控制。
#### gamepad
手柄有关的操作，详见[gamepadex](gamepadex.md)