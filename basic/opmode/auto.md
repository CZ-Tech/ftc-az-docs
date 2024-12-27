# auto:自动阶段代码

## 概要

我们通过```driveStraight```和```driveStrafe```两个函数来让机器分别进行前进、后退，以及向左、向右平移。```turnToHeading```函数来让他调整朝向。以及```sleep```让机器停止运动。

## 参数列表

- ```distance```：机器要行走的距离。
- ```time```：机器执行这一任务的时间，单位为毫秒，主要用于```sleep```函数。
- ```power```：机器执行任务时电机的功率。
- ```heading```：机器需要运转的角度

## 具体介绍

### driveStraight

通过这个函数来实现机器以**自身位置**为参照，进行前后移动，distance为正，则机器向前运动，为负则向后运动。同时，在运动的过程中还可以进行转向，但是可能会造成一定的误差。

**示例代码：**

```java
robot.drivetrain
    .driveStraight(double distance, double heading, double power)
;
```

### driveStrafe

通过这个函数来实现机器以**自身位置**为参照，进行左右移动，distance为正，则机器向左运动，为负则向右运动。同时，在运动的过程中还可以进行转向，但是可能会造成一定的误差。

**示例代码：**

```java
robot.drivetrain
    .driveStrafe(double distance, double heading, double power)
;
```

### turnToHeading

通过这个函数，我们可以调整机器的转向，可以使机器较精准地运动。

**示例代码：**

```java
robot.drivetrain
    .turnToHeading(double heading, double power)
;
```

### sleep

通过这个函数让机器静止。

```java
robot.drivetrain
    .sleep(double time)
;
```