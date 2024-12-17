# teleop:手动阶段程序

## 概要

### 路径

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
    .keyPress("a", () -> telemetry.addLine("Button.A - Pressed"))//按下a
    .keyUp("a", () -> telemetry.addLine("Button.A - KeyUp"))//松开a
    .keyDown("a", () -> telemetry.addLine("Button.A - KeyDown"))//按下a的瞬间
    .keyToggle("cross",
            () -> System.out.println("Button.A - KeyToggle 1"),
            () -> System.out.println("Button.A - KeyToggle 2")
    )//x键切换功能
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


### 手柄摇杆曲线

如果操作手觉得手柄的手感比较滑或者涩，那么可以直接删除/更改该函数。

这对程序没有任何影响。