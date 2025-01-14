# auto:code of auto phase
**Route:**
> Teamcode/java/org.firsinspires.ftc.teamcode/opmode/auto

## abstract

We mainly use ```driveStrafe()``` method to make the robot move left and right, ```driveStraight()``` method to make the it move back and forth, ```sleep```method to make it freeze, and ```turnToHeading``` method to adjust its orientation.

## Details

Details can be seen in [drivetrain:底盘控制](basic/drivetrain.md).

#### Parameter list
- ```distance```: The distance the robot is to travel.
- ```time```: The time in milliseconds for the robot to perform this task, mainly used in the ```sleep``` function.
- ```power```: The power of the motor when the machine performs the task.
- ```heading```: The angle by which the machine needs to turn.

#### driveStraight
This method is used to realize that the machine moves backwards and forwards with **its own position** as a reference, a positive distance moves the machine forwards and a negative distance moves it backwards. At the same time, in the process of movement, the robot itself can also turn, but may cause some error.

**Example:**
```java
robot.drivetrain
    .driveStraight(double distance, double heading, double power)
;
```

#### driveStrafe
This method is used to realize that the machine moves right and left with **its own position** as a reference, a positive distance moves the machine right and a negative distance moves it left. At the same time, in the process of movement, the robot itself can also turn, but may cause some error.

**Example:**

```java
robot.drivetrain
    .driveStrafe(double distance, double heading, double power)
;
```

#### turnToHeading
 With this method, we can adjust the orientation of the robot which can make the machine move more accurately.

**Example:**

 ```java
robot.drivetrain
    .turnToHeading(double heading, double power)
;
```
### sleep
We can use this mathod to make the robot still.
```java
robot.drivetrain
    .sleep(double time)
;
```