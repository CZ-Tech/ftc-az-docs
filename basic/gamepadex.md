# gamepadEX:手柄参数

## 概要
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
在链式调用，都需要将gamepad进行一次更新。
### keyPress
```java
public GamepadEx keyPress(String key, Runnable fn) {
    if (getKey(currGamepad, key)) fn.run();
    return this;
}
```
当某一个特定按键按着时，会运行一个函数。主要用于控制机器的运动。
### keyDown
```java
public GamepadEx keyDown(String key, Runnable fn) {
    if (getKey(currGamepad, key) && !getKey(prevGamepad, key)) fn.run();
    return this;
}
```
当某一个特定按键按下时，会运行一个函数。
### keyUp
```java
public GamepadEx keyUp(String key, Runnable fn) {
    if (!getKey(currGamepad, key) && getKey(prevGamepad, key)) fn.run();
    return this;
}
```
当某一个特定按键松开，会运行一个函数。
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
按下按键时，函数运行一次，刷新一次状态（运行另一个函数）。例如在进行抓取时，，按下特定的按键时，爪子会进入松开或者关闭的状态，第二次按下按键时，状态会发生改变
