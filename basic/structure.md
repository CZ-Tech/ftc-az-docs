# 程序结构

## 代码位置
> FtcRobotController\TeamCode\src\main\java\org\firstinspires\ftc\teamcode
## 代码结构

```
teamcode
├─common
│  │  Globals.java
│  │  Robot.java
│  ├─command
│  │      Command.java
│  ├─drive
│  │      Drivetrain.java
│  ├─hardware
│  │      GamepadEx.java
│  ├─subsystem
│  │      Subsystem.java
│  ├─util
│  │      Alliance.java
│  │      OpModeState.java
│  └─vision
│      │  Vision.java
│      └─pipeline
└─opmode
    ├─auto
    │      Auto.java
    └─teleop
            Duo.java
            Solo.java
```


## 说明

<!-- **在代码中调用函数时请使用robot.\<module>.\<method>** -->

### Globals.java
该文件包含了程序中常用的一些常量，使用前必须根据自己的机器进行调整

### Robot.java
该文件是所有模块的统一入口，整合了各部分的内容。

### Drivetrain.java
该文件包含机器人底盘的移动代码，适用于机器整体的移动。

### GamepadEx.java
该文件包含了对于FTC SDK中手柄检测的拓展，简化对手柄的编程。

### Subsystem.java
该文件是对所有子系统模块的统一入口，整合了各个子系统的内容。

### Command.java
该文件包含了多个子系统共同实现的功能，通常会把一系列各个子系统的具体动作放在这里进行整理。比如在抬起机械臂后，松开爪子，然后收起机械臂等一连串动作。

### Auto.java
该文件是自动阶段的代码。

### Duo.java
该文件是双人模式下手动阶段的代码。

### Solo.java
该文件是单人模式下手动阶段的代码。