# gamepadEX:手柄扩展

## 概要

我们在询问过操作员后，发现按键按下、放开、一直按着和切换比较常用，所以封装了**keyPress**、**keyDown**、**keyUp**和**keyToggle**，简化了手柄按键的检测，并且实现了链式调用，让代码更加简洁、易懂。

## 路径

> Teamcode/java/org.firsinspires.ftc.teamcode/ common / hardware / GamepadEx

## 具体介绍
### 参数列表
- ```key```: 检测的按键，与```FTC SDK```中手柄按键名称一致，```String```类型
- ```Runnable```: 要运行的函数，建议使用**Lambda表达式**，```Runnnable```类型

### update
每次定义手柄按键时都需要先运行一次，用来更新手柄状态。否则每次循环都会使用上次状态，无法判断按键状态。
**示例代码**
```java
robot.gamepad1
    .update()//更新状态
    .<other methods>
;
```

### keyPress
当按下key时，执行```Runnable```。注意：```Runnable```在```key```按下的期间会**循环运行**。

**示例代码**
```java
robot.gamepad1
    .update()
    .keyPress("a",Runnable)//按住a键
;
```

### keyDown
当按下```key```时，执行```Runnable```。注意：```Runnable```在```key```按下的瞬间只**运行一次**。

**示例代码**
```java
robot.gamepad1
    .update()
    .keyDown("a",Runnable)//按下a键
;
```

### keyUp
当按下```key```时，执行```Runnable```，并进行下一轮判断。注意：```Runnable```在```key```抬起的瞬间只**运行一次**。

**示例代码**
```java
robot.gamepad1
    .update()
    .keyUp("a",Runnable)//抬起a键
;
```

### keyToggle
当按下key时，执行一次```Runnable1```的内容；再次按下```key```，执行一次```Runnable2```的内容，并如此循环。

**示例代码**
```java
robot.gamepad1
    .update()
    .keyToggle("a",Runnable1, Runnable2)//按下a键切换
;
```

**建议在切换的函数中增加遥测的信息显示以确认当前状态**