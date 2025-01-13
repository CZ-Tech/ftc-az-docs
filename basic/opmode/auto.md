# auto:自动阶段代码
路径：
> Teamcode/java/org.firsinspires.ftc.teamcode/opmode/auto

## 概要
我们通过```driveStraight```和```driveStrafe```两个函数来让机器分别进行前进、后退，以及向左、向右平移。```turnToHeading```函数来让他调整朝向。以及```sleep```让机器停止运动。

## 具体介绍

### 运动模块
详见[drivetrain:底盘控制](basic/drivetrain.md)

#### 参数列表
- ```distance```：机器要行走的距离。
- ```time```：机器执行这一任务的时间，单位为毫秒，主要用于```sleep```函数。
- ```power```：机器执行任务时电机的功率。
- ```heading```：机器需要运转的角度



#### driveStraight

通过这个函数来实现机器以**自身位置**为参照，进行前后移动，distance为正，则机器向前运动，为负则向后运动。同时，在运动的过程中还可以进行转向，但是可能会造成一定的误差。
**示例代码：**
```java
robot.drivetrain
    .driveStraight(double distance, double heading, double power)
;
```

#### driveStrafe
通过这个函数来实现机器以**自身位置**为参照，进行左右移动，distance为正，则机器向左运动，为负则向右运动。同时，在运动的过程中还可以进行转向，但是可能会造成一定的误差。

**示例代码：**

```java
robot.drivetrain
    .driveStrafe(double distance, double heading, double power)
;
```

#### turnToHeading
通过这个函数，我们可以调整机器的转向，可以使机器较精准地运动。

**示例代码：**

```java
robot.drivetrain
    .turnToHeading(double heading, double power)
;
```

#### sleep
通过这个函数让机器静止。
```java
robot.drivetrain
    .sleep(double time)
;
```

### 上层模块

路径：> Teamcode/java/org.firsinspires.ftc.teamcode/common/subsystem

我们在子系统栏目编辑这一部分的程序，以arm机械臂的编写为例：

首先，我们对于机器以及涉及该部分的电机进行定义
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
**以下是armmotor.setMode(DcMotor.RunMode.---)中不同的模式的用途:**
|  名称  | 用途   | 优劣 |
|:------:|:------:|:---:|
|RUN_WITHOUT_ENCODERS  | 仅仅通过编写的时间与路程来让电机运行，此过程中编码器不起作用 | 方便编写，但不能在运行过程中考虑到摩擦力、电池电量等因素，可能造成其其运行不精准|
|RUN_USING_ENCODER     |电机保持恒定的速度，不会因电池电量而改变。通过监测每秒经过多少个刻度，电机就能在设定的时间内保持相同的速度。| 路程、速度便于控制 |
|RUN_TO_POSITION       |侧重于电机的旋转位置。该设置可用于为电机旋转到的位置设定一个编码器值，然后使电机旋转到该编码器值所代表的位置。|/|
 |STOP_AND_RESET_ENCODER| 将电机编码器的值重置为 0。这不会使电机移动，而只是使电机当前所处的编码器位置成为新的 0。|/|

**以下是setZeroPowerBehavior(DcMotor.ZeroPowerBehavior.---)中不同模式所代表的状态：**
|  名称  | 含义    |
|:--------:|:----------:|
|UNKNOWN  | 在功率等于0时的状态未知 |
|BRAKE     | 在功率等于0时，电机锁死，拒绝任何外力对他的状态进行更改 | 
|FLOAT  |    在功率等于0时，电机接受任何外力的旋转 |

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

完成底层代码书写，我们就可以来将底层代码中封装的方法进入auto这个文件中进行调用，完成程序的编写。