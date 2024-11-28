# gamepadEX:手柄参数

## 概要
**路径：Teamcode/Java/org.firstinspires.ftc.teamcode/drive/Drivetrain**

由于传统的上升沿检测器与下生沿检测器编写过于繁杂，我们在询问过操作员后，发现按键按下、放开、一直按着和切换比较常用，所以封装了**keyPress**、**keyDown**、**keyUp**和**keyToggle**，简化了手柄按键的检测，实现了链式调用，并且让代码更加简洁、易懂。
## 具体介绍
### 参数列表
- key:检测的按键，与FTC SDK中手柄按键名称一致，String类型
- fn:要运行的函数，建议使用**Lambda表达式**，Runnnable类型
### update
```java
public GamepadEx update() {
    prevGamepad.copy(currGamepad);
    currGamepad.copy(gamepad);
    return this;
}
```
每次判断手柄按键时都需要先运行一次，用来更新手柄状态。
### keyPress
```java
public GamepadEx keyPress(String key, Runnable fn) {
    if (getKey(currGamepad, key)) fn.run();
    return this;
}
```
当按下key时，执行fn的内容，并进行下一轮判断。注意：fn在key按下的期间会循环运行。
### keyDown
```java
public GamepadEx keyDown(String key, Runnable fn) {
    if (getKey(currGamepad, key) && !getKey(prevGamepad, key)) fn.run();
    return this;
}
```
当按下key时，执行fn的内容，并进行下一轮判断。注意：fn在key按下的瞬间只运行一次。
### keyUp
```java
public GamepadEx keyUp(String key, Runnable fn) {
    if (!getKey(currGamepad, key) && getKey(prevGamepad, key)) fn.run();
    return this;
}
```
当按下key时，执行fn的内容，并进行下一轮判断。注意：fn在key抬起的瞬间只运行一次。
### keyToggle
```java
public GamepadEx keyToggle(String key, Runnable fn1, Runnable fn2){
    keyState.putIfAbsent(key, false);
    if (getKey(currGamepad, key) && !getKey(prevGamepad, key)){
        keyState.computeIfPresent(key, (k, v) -> !v);
        if (keyState.getOrDefault(key, false)){
            fn1.run();
        }else{
            fn2.run();
        }
    }
}
```
当按下key时，执行一次fn1的内容；再次按下key，执行一次fn2的内容，并如此循环。
### 代码示例
```java
robot.gamepad1
    .update()
    .keyPress("a", () -> telemetry.addLine("Button.A - Pressed"))//按下a
    .keyUp("a", () -> telemetry.addLine("Button.A - KeyUp"))//松开a
    .keyDown("a", () -> telemetry.addLine("Button.A - KeyDown"))//按下a的瞬间
    .keyToggle("cross",
            () -> System.out.println("Button.A - KeyToggle 1"),
            () -> System.out.println("Button.A - KeyToggle 2")
    )//x键切换功能
            ;
```