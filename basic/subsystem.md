# subsystem: 子系统

## 概要

路径：> Teamcode/java/org.firsinspires.ftc.teamcode/common/subsystem

我们开设了subsystem文件，将机器除了运动模块之外所分装的函数规整在一起，包括机械臂、爪子等等。通过开设这样的一个文件，可以使代码更具有逻辑性与可读性，也方便进行调用。

## 详细介绍

首先，我们在subsystem文件中，新建一个子文件，并给他取一个生动形象的名字，再在其中导入一些需要用到的库；在其中Subsystem子文件中加入结构的名称。以机械臂arm为例：

```java
public class Subsystem {
    public Arm arm;
    public final Robot robot;
    public Subsystem(Robot robot) {
    this.robot = robot;
    this.arm = new Arm(robot);
    }
}

```

其次，回到新建的文件之中，对于涉及该部分的电机进行定义、命名、以及初步的设置：

```java
private final Robot robot;
private DcMotorEx armmotor;

public Arm(Robot robot) {
    this.robot = robot;
    armmotor = robot.hardwareMap.get(DcMotorEx.class, "armmotor");
    //通过hardwareMap，可根据机器人配置时关联的相应物理设备名称，检索运行时的 HardwareDevice 实例。
    armmotor.setMode(DcMotor.RunMode.RUN_WITHOUT_ENCODER);
    //RUN_WITHOUT_ENCODERS 表示电机不使用编码器，而是用给定的速度和时间运行。
    armmotor.setZeroPowerBehavior(DcMotor.ZeroPowerBehavior.BRAKE);
    //设置机器在0功率下的状态
    }
```

接下来可以设置各种不同的任务，比如：
```java
public Arm up() {
    armmotor.setPower(1);
    return this;
}
```

**完整示例代码：**
```java
public class Arm {

    private final Robot robot;
    private DcMotorEx armmotor;

    public Arm(Robot robot) {
        this.robot = robot;
        armmotor = robot.hardwareMap.get(DcMotorEx.class, "armmotor");
        armmotor.setMode(DcMotor.RunMode.RUN_WITHOUT_ENCODER);
        armmotor.setZeroPowerBehavior(DcMotor.ZeroPowerBehavior.BRAKE);
    }

    public Arm up() {
        armmotor.setPower(1);
        return this;//支持链式调用
    }
}
```
完成这些代码的编写后，我们就能在各个代码中调用，实现各种功能了。