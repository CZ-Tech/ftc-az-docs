# drivetrain:底盘控制

## 概要
### 路径
> drive/Drivetrain

本文件包含了各种与机器人底层运动相关的函数，通过robot.Drivetrain进行调用。
## 链式调用
我们的代码库中一大特点就是支持链式调用，也就是不需要写冗长的代码而精简为一连串函数的连续调用。这种方式大大减少了代码量，并且封装的函数使得用户不需要知道具体的实现逻辑，便于编写。
下面是一些支持链式调用的函数：
### Drivetrain resetYaw()
这个函数可以重置机器的朝向，一般会在INIT阶段后手动阶段前调用：
```java
@Override
public void runOpMode() {
    //等待开始
    waitForStart();
    robot.drivetrain.resetYaw();

    /*主要移动逻辑*/
}
```
### Drivetrain driveStraight(double distance, double heading, double speed)
参数列表：
- distance:移动距离
- heading:当前朝向
- speed:移动速度

这个函数用于让机器人前后移动，并且可以设置移动速度。一般会和```driveStrafe()```函数一起使用。
### Drivetrain driveStrafe(double distance, double heading, double speed)
这个函数用于让机器人左右移动，并且可以设置移动速度。一般会和```driveStraight()```函数一起使用：
```java
robot.drivetrain
    .driveStraight(24.0, 0.0, 1.0)
    .sleep(1000)//停止移动
    .driveStrafe(24.0, 0.0, 1.0)
    .sleep(1000)//停止移动
;
```
### Drivetrain rush(double distance, double heading)
参数列表：
- distance:移动距离
- heading:当前朝向

这个函数让机器人以全速移动，并且附有加速与减速过程，防止打滑
### Drivetrain sleep(long milliseconds)
这个函数可以让机器人暂停，其中时间以毫秒为单位。
```java
robot.drivetrain
    .driveStraight(24.0, 0.0, 0.5)
    .sleep(1000)
    .driveStrafe(24.0, 0.0, 0.5)
    .sleep(1000)
    .holdHeading(0,0.5,1);
```
### Drivetrain turnToHeading(double heading, double speed, double timeout, double P_DRIVE_GAIN)
这个函数可以让机器人以自身为中心转到特定的角度。

函数重载如下：
- Drivetrain turnToHeading(double heading, double speed, double timeout)
- Drivetrain turnToHeading(double heading, double speed)
### Drivetrain holdHeading(double heading, double speed, double holdTime)
这个函数可以让机器人以自身为中心转到特定的角度并停留一段时间。
## 多种手动阶段移动方式
除了支持链式调用外，我们的代码库也提供了不同的针对手动阶段的移动方式：
### void driveRobot(double axial, double lateral, double yaw)
参数列表：
- axial:前后移动
- lateral:左右移动
- yaw:旋转方向

这个函数是经典的麦克纳姆轮的驱动函数，以手柄的摇杆作为输入信号：

这种方式更适用于**第一人称控制**。
### void driveRobotFieldCentric(double axial, double lateral, double yaw)
参数列表：
- axial:前后移动
- lateral:左右移动
- yaw:旋转方向

如果你不习惯或者只是单纯不喜欢使用传统移动函数，我们的代码库还包含基于场地坐标系的移动函数。这种移动方式的好处在于机器人总是按照操作员的意愿移动(而不是单纯地向机器人的前方移动)，其参考系是整个场地，因此更加可控。

这种方式更适用于**第三视角控制**。
## 一些常用的运动函数
除了上面的函数之外，我们还添加了许多控制底层运动逻辑的函数：
### void stopMotor()
停止所有电机。
### double getHeading()
获取机器当前朝向。
### void setRunMode()
设置电机运行模式
### void setDrivePower(double leftFrontPower, double rightFrontPower, double leftBackPower, double rightBackPower)
设置四个轮子的电机功率。