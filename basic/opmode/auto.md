# auto:code of auto phase
**Route:**
> Teamcode/java/org.firsinspires.ftc.teamcode/opmode/auto

## Abstract

We mainly use ```driveStrafe()``` to make the robot move left and right, ```driveStraight()``` to make the it move back and forth, ```sleep```method to make it freeze, and ```turnToHeading``` to adjust its orientation.

## Details

Details can be seen in [drivetrain:底盘控制](basic/drivetrain.md).

### Parameter list
- ```distance```: The distance the robot is to travel.
- ```time```: The time in milliseconds for the robot to perform this task, mainly used in the ```sleep``` function.
- ```power```: The power of the motor when the machine performs the task.
- ```heading```: The current heading of the robot.

### DriveStraight
This method is used to realize that the machine drives backwards and forwards with **its own position** as a reference, a positive distance drives the machine forwards and a negative distance drives it backwards. At the same time, in the process of movement, the robot itself can also turn, but may cause some error.

**Example:**
```java
robot.drivetrain
    .driveStraight(double distance, double heading, double power)
;
```

### DriveStrafe
This method is used to realize that the machine drives right and left with **its own position** as a reference, a positive distance drives the machine right and a negative distance drives it left. At the same time, in the process of movement, the robot itself can also turn, but may cause some error.

**Example:**

```java
robot.drivetrain
    .driveStrafe(double distance, double heading, double power)
;
```

### TurnToHeading
 With this method, we can adjust the orientation of the robot which can make the machine move more accurately.

**Example:**

 ```java
robot.drivetrain
    .turnToHeading(double heading, double power)
;
```
### Sleep
We can use this mathod to make the robot still.
```java
robot.drivetrain
    .sleep(double time)
;
```