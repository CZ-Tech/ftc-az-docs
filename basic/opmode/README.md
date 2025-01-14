# opmode:自动与手动阶段设计

## 链式调用
在我们的自动阶段与手动阶段的代码中，我们支持链式调用，大大减少了代码量与编写效率，支持链式调用的函数可以参考[drivetrain:底盘控制](basic/drivetrain.md)
## 统一入口

我们编写程序统一入口，可以通过driverhub来选择自动阶段的起始位置、联盟的颜色以及操作者的数量，从而进入相应的程序。

```java 
   @TeleOp(name = "Solo🔴", group = "Solo")public static class SoloRed extends TeleOpMode {@Overridepublic void runOpMode() {
        robot.teamColor = Alliance.RED;
        robot.opModeState = OpModeState.Solo;super.runOpMode();
    }
}

@TeleOp(name = "Solo🔵", group = "Solo")public static class SoloBlue extends TeleOpMode {@Overridepublic void runOpMode() {
        robot.teamColor = Alliance.BLUE;
        robot.opModeState = OpModeState.Solo;super.runOpMode();
    }
}

@TeleOp(name = "Duo🔴", group = "Duo")public static class DuoRed extends TeleOpMode {@Overridepublic void runOpMode() {
        robot.teamColor = Alliance.RED;
        robot.opModeState = OpModeState.Duo;super.runOpMode();
    }
}

@TeleOp(name = "Duo🔵", group = "Duo")public static class DuoBlue extends TeleOpMode {@Overridepublic void runOpMode() {
        robot.teamColor = Alliance.BLUE;
        robot.opModeState = OpModeState.Duo;super.runOpMode();
    }
}
```