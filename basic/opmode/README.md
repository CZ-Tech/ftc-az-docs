# Opmode: code for auto and teleop

## Chains

Our code for automatic phase and manual phase supports chains, which greatly reduces the amount of code and improves programming efficiency. You can refer to [drivetrain:底盘控制](basic/drivetrain.md) to get detailed information about methods supporting chains.

## Unified entrance

We write programs with a unified entrance, through which wecan select different code including diffrent starting positions of the automated phase, the colours of the union, and the numbers of operators via driverhub, which can bring us much convenience. Specific codes are listed below.

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