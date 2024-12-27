# opmode:自动与手动阶段设计


## 链式调用
在我们的自动阶段与手动阶段的代码中，我们支持链式调用，大大减少了代码量与编写效率，支持链式调用的函数可以参考[gamepadEX:手柄扩展](basic/gamepadex.md)

## 统一入口

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