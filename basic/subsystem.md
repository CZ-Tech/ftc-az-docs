# Subsystem

## Abstact

**Route:**
> Teamcode/java/org.firsinspires.ftc.teamcode/common/subsystem

We created a subsystem file to intergrate the methods of the robot except for the motion module, including the arm, the claw, etc. The file was created to make the code more logical and readable, as well as easier to invoke.

## Details

First of all, we should create a new sub-file in the ```Subsystem```, and give him a vivid name, and then import some of the libraries needed using; In the ```Subsystem``` sub-file,  add the name of the structure. Take the robotic arm for example:

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

Next, go back to the newly created file and define, name, and initially set up the motors involved in the section:

```java
private final Robot robot;
private DcMotorEx armmotor;

public Arm(Robot robot) {
    this.robot = robot;
    armmotor = robot.hardwareMap.get(DcMotorEx.class, "armmotor");
    //HardwareMap provides a means of retrieving runtime HardwareDevice instances according to the names with which the corresponding physical devices were associated during robot configuration. 
    armmotor.setMode(DcMotor.RunMode.RUN_WITHOUT_ENCODER);
    //RUN_WITHOUT_ENCODERS indicates that the motor does not use an encoder, but runs at the given speed and time.
    armmotor.setZeroPowerBehavior(DcMotor.ZeroPowerBehavior.BRAKE);
    //设置机器在0功率下的状态
    //set the state of motor in 0 power
    }
```

Then we can set various tasks for the structure. For example: 

```java
public Arm up() {
    armmotor.setPower(1);
    return this;
}
```

**Complete sample code:**

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

After programming these codes, we can invoke the in the various codes to implement various functions.