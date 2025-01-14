# Globals: Robot basic constants

## Abstract

**Route:**
> Teamcode/java/org.firsinspires.ftc.teamcode/common/Globals

These basic constants directly affect the motion of the robot, so it is important to fill in proper values.

## Details

### COUNTS_PER_MOTOR_REV
COUNTS_PER_MOTOR_REV is a constant that describe how many counts the wheel makes per revolution.

Rev HD Hex Motor (No Gearbox) : 28 counts/revolution

**Formula:**

reduction-gear-box*counts-per-revolution=COUNTS_PER_MOTOR_REV

eg: GoBILDA 312 RPM (19.2:1) Yellow Jacket 537.6=28*19.2
40:1 Rev 28*40=1120
20:1 Rev 28*20=560
Calculate the COUNTS_PER_INCH for your specific drive train.




**It is also recommended to your motor vendor website to determine your motor's COUNTS_PER_MOTOR_REV**

### DRIVE_GEAR_REDUCTION

For external drive gearing, set DRIVE_GEAR_REDUCTION as needed. If you don't install an external gearbox, set this constant as 1.0.

If there is an external one, use a value of 2.0 for a 12-tooth spur gear driving a 24-tooth spur gear and so on.

This is gearing DOWN for less speed and more torque.

For gearing UP, use a gear ratio less than 1.0. Note this will affect the direction of wheel rotation.

### WHEEL_DIAMETER_INCHES

Enter the diameter of the wheel in inches, or you can find that information on retail websites.

### ODO_COUNTS_PER_INCH

The counts of each revolution of the odometer is an important constant for the correction of machine movements.

**Formula:**

ODO_COUNTS_PER_INCH = COUNTS_PER_ODO_REV / (WHEEL_DIAMETER_INCHES * Math.PI);

### P_TURN_GAIN

We normalising the power of motor between [-1,1] and transmitting the signal to the motor by multiplying this value by the error in the actual rotation.

Therefore, if this value is too large, the turning speed will be too high, resulting in inaccurate turns, and too small a value will result in a long turning time.

**It is recommended to get the value that works for you in multiple tries**

### HEADING_THRESHOLD

This value is used to determine the acceptable error when turning.

In our code, we compare the turning error with this value. If the error value is less than this value, then the correction is completed and the next procedure can be carried out; if the error value is greater than this value, then the machine continues to correct its heading until the error value falling within the specified range.

Therefore, if this value is too large, it will lead to inaccurate turning. And if the value is too small, it will lead to repeated correction, which will affect the subsequent procedure.

**It is recommended to get the value that works for you in multiple tries**