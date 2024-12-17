# auto:自动阶段代码

## 概要

路径：opmode/auto

我们用```Trajectory```函数，并对原有的代码进行封装，成为```addPoint```，```addVelocity```,两个函数，通过输入运动结束的时间点、x、y方向的初速度与末速度以及初位置和末位置，来去确定运动的路径，从而达到运动的效果。

## 具体介绍

### 参数列表

* ```t```：运动结束的时间点。
* ```x```：运动结束时的横坐标。
* ```y```：运动结束时的纵坐标。
* ```dx```：运动结束时横坐标方向的速度。
* ```dy```：运动结束时纵坐标方向的速度。

### startPosition(startPosition)

这个函数用来设置机器的初位置，是每一条自动阶段代码前必要的声明,以便于接下来机器的运动。

#### 示例代码：
```java
trajectory.startMove(startPosition)
    .RunnableFunction
    
```


### addPoint

这个函数用于表达机器机器的最终位置以及速度，这个位置/速度既是这一个时刻的位置/速度，也是下一个运动的初位置/初速度。

#### 示例代码：
```java
 trajectory.startMove(startPosition)
    .addPoint(t, x, y, dx, dy)
```

### addVelocity

这个函数用于设置下一次运动的初速度，让机器可以从下一个运动开始时进行曲线运动。

示例代码：

```java
trajectory.startMove(startPosition)
    .addVelocity(dx, dy)