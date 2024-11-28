# Globals:机器人基本参数

路径：Teamcode>Java>org.firstinspires.ftc.teamcode>common>vision>Globals

这些基本参数直接影响到机器人的运动，所以填写恰当的数值是十分重要的。
## COUNTS_PER_MOTOR_REV
转一圈的计数，常见的电机及其计数为：

Rev HD Hex Motor，28次。

GoBILDA:312次（19.2：1）

40：1REV：28×40=1120次

## DRIVE_GEAR_REDUCTION
外部齿轮减速，如果使用电机减速箱而没有加装齿轮的话值为1。

## WHEEL_DIAMETER_INCHES
输入轮子的直径，单位为英寸

## HEADING_THRESHOLD
转向时允许的误差，如果值过大会导致转向不精确，值过小会导致转向调整过于频繁而浪费时间。

**推荐在多次尝试中得到适合自己的值**。