# Drivetrain

## abstract

**Route:**
 > Teamcode/java/org.firsinspires.ftc.teamcode/common/drive/Drivetrain
 
 This file contains various methods related to the drivetrain of the robot, which can be invoked via ```robot.Drivetrain```.

 ## chains
One of the major features of our code is the support for chains, so that there is no need to write long code but we can simplify our codes by invoking a series of methods. Programmer don't need to remember the specific logic of the code eiither, which can benifit new learners and improve the efficiency of programming.

Here are some methods that support chains:
### Drivetrain resetYaw()
This method resets the orientation of the machine and is typically ivoked before the manual phase after the INIT phase:
```java
@Override
public void runOpMode() {
    //wait for start
    waitForStart();
    robot.drivetrain.resetYaw();

    /*Primary Mobile Logic*/
}
```
### Drivetrain driveStraight(double distance, double heading, double speed)
Parameter list:
- distance: distance to cover
- heading: current heading
- speed: the speed of robot

This method is used to make the robot move back and forth, and allows you to set the speed of the movement. It is usually used with ```driveStrafe()```.

### Drivetrain driveStrafe(double distance, double heading, double speed)
This method is used to make the robot move left and right, and allows you to set the speed of the movement. It's usually used with ```driveStraight()``` .：
```java
robot.drivetrain
    .driveStraight(24.0, 0.0, 1.0)
    .sleep(1000)//stop moving
    .driveStrafe(24.0, 0.0, 1.0)
    .sleep(1000)//stop moving
;
```
### Drivetrain rush(double distance, double heading)
Parameter list:
- distance: distance to cover
- heading: current heading

This function allows the robot to move at full speed with acceleration and deceleration to prevent slippage.

### Drivetrain sleep(long milliseconds)
This method allows the robot to pause, where time is measured in milliseconds.
```java
robot.drivetrain
    .driveStraight(24.0, 0.0, 0.5)
    .sleep(1000)
    .driveStrafe(24.0, 0.0, 0.5)
    .sleep(1000)
    .holdHeading(0,0.5,1);
```

### Drivetrain turnToHeading(double heading, double speed, double timeout, double P_DRIVE_GAIN)
This method allows the robot to turn to a specific angle centred on itself.

The methods are overloaded as follows:
- Drivetrain turnToHeading(double heading, double speed, double timeout)
- Drivetrain turnToHeading(double heading, double speed)

### Drivetrain holdHeading(double heading, double speed, double holdTime)
This method allows the robot to turn to a specific angle centred on itself and stay there for a period of time.

## Multiple manual stage movement methods
In addition to methods supporting chains, our codes also provide different ways of motion at manual stages:

### void driveRobot(double axial, double lateral, double yaw)
Parameter list:
- axial: forward/backward movement
- lateral:l eft-right movement
- yaw: angle to turn by

This method is the classic drive method for a McNamee wheel, using the gampad as the input signal:

**Robot itself is the coordinate origin.**
### void driveRobotFieldCentric(double axial, double lateral, double yaw)
Parameter list:
- axial: forward/backward movement
- lateral: left-right movement
- yaw: deriction

If you are not used to, or just simply don't like, using traditional mobile methods, our codes also include mobile methods based on the field coordinate system. The advantage of this type of method is that the robot always moves as the operator wants it to (rather than simply to the front of the robot), which means its reference system is the entire field, making it more controllable.

**The coordinate origin is set in the field and not changed easily as the robot move.**

## Some common motion methods
In addition to the methods above, we have added a number of methods that control the motion of robots:
### void stopMotor()
Stop all motors.
### double getHeading()
Get the current heading of robots.
### void setRunMode()
Set the state of  motors.
### void setDrivePower(double leftFrontPower, double rightFrontPower, double leftBackPower, double rightBackPower)
Set the power of four wheels.