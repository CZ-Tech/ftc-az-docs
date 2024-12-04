# Robot:万物之源

## 概要
Robot.java包含了所有机器人模块，作为代码的统一入口使用。这样就可以将重复的代码重写成函数调用，并更具可读性。
### 路径
> common\Robot.java
## 说明
### 初始化
在手动或自动代码中，都需要先定义Robot对象：
```java
Robot robot = new Robot();
```
然后，在```runOpMode()```中使用```robot.init(this)```初始化Robot对象：
```java
@Override
public void runOpMode() {
    robot.init(this);
    /*Main Methods*/
}
```
### 使用
作为统一入口，所有对机器人的控制都可以通过```robot.\<module>.\<method>```进行调用，并且部分代码支持链式调用，示例如下：
```java
robot.drivetrain.driveStrafe(-65.0, 0, DRIVESPEED);//移动模块
robot.subsystem.slamDunker.grab();//子系统调用
robot.gamepad1.update();//手柄模块
/*Other Methods*/
```
### 详细解释
Robot.java中包含了机器的所有模块入口，下面介绍一些常用的模块：
#### hardwareMap
通过Driver Hub上编辑的硬件名称获取硬件。
#### telemetry
Driver Hub上的遥测，用于显示信息。
#### drivetrain
用于机器底层移动，详见[drivetrain](drivetrain.md)
#### subsystem
机器的子系统，包含上层的控制。
#### gamepad
手柄有关的操作，详见[gamepadex](gamepadex.md)