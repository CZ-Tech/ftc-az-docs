# teleop:手动阶段程序

## 概要

路径：

> opmode/teleop

我们在询问过操作员后，发现按键按下、放开、一直按着和切换比较常用，所以封装了**keyPress**、**keyDown**、**keyUp**和**keyToggle**，简化了手柄按键的检测，并且实现了链式调用，让代码更加简洁、易懂。

## 具体介绍
### 参数列表
- key:检测的按键，与```FTC SDK```中手柄按键名称一致，```String```类型
- fn:要运行的函数，建议使用**Lambda表达式**，```Runnnable```类型


### 手柄定义
```java
robot.gamepad1
    .update()
    .keyPress("a",Runnable)//按下a
    .keyUp("b",Runnable)//松开b键
    .keyDown("x",Runnable)//按住x键
    .keyToggle("y",Runnable1, Runnable2)//按下y键切换
    
;
```
对手柄上的按键进行定义。详情可见 [gamepadEX:手柄扩展](basic/gamepadex.md)

### 统一入口

我们编写程序统一入口，可以通过driverhub来选择自动阶段的起始位置、联盟的颜色以及操作者的数量，从而进入相应的程序。

```java 
    @TeleOp(name = "Duo/Solo Colour", group = "Duo/Solo")//进入Duo（多个操作者的适用程序）或者Solo（单个操作者的适用程序）
    public static class Duo/SoloColour extends Duo/Solo {//输入人数+颜色
        @Override
        public void runOpMode() {
            robot.teamColor = Alliance.Colour;//输入颜色
            super.runOpMode();
        }
    }
```

### 场地中心坐标系

我们通过```robot.drivetrain.driveRobotFieldCentric()```函数让机器以场地中心坐标来确定自己的方向，但是在实际操作的过程中，操作手可能由于各种原因不了解机器的方向，因此需要使用重新定义一个按键，来重置场地坐标。

```java
robot.drivetrain.driveRobotFieldCentric(
        gamepad1.left_stick_y,
        gamepad1.left_stick_x,
        gamepad1.right_stick_x
);
```
如果不习惯场地中心坐标，可以使用```robot.drivetrain.driveRobot()```函数，让机器以自身为坐标。

```java
robot.drivetrain.driveRobot(
        gamepad1.left_stick_y,
        gamepad1.left_stick_x,
        gamepad1.right_stick_x
);
```

**选取哪种方法取决于操作手的习惯。**

### 手柄摇杆曲线

如果操作手觉得手柄的手感比较滑或者涩，那么可以直接删除/更改该函数。
```java
private double sss(double v) {
    if (v > 0.0) { //若手柄存在中位漂移或抖动就改0.01
        v = 0.87 * v * v * v + 0.09;//0.13是23-24赛季底盘启动需要的功率
    } else if (v < 0.0) { //若手柄存在中位漂移或抖动就改-0.01
        v = 0.87 * v * v * v - 0.09; //三次方是摇杆曲线
    } else {
        // XBOX和罗技手柄死区较大无需设置中位附近
        // 若手柄存在中位漂移或抖动就改成 v*=13
        // 这里的13是上面的0.13/0.01=13
        v = 0;
    }
    return v;
}
```
这对程序没有任何影响。