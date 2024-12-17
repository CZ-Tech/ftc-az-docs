# gamepadEX:手柄扩展

## 概要
### 路径
> drive/Drivetrain

我们在询问过操作员后，发现按键按下、放开、一直按着和切换比较常用，所以封装了**keyPress**、**keyDown**、**keyUp**和**keyToggle**，简化了手柄按键的检测，并且实现了链式调用，让代码更加简洁、易懂。
## 具体介绍
### 参数列表
- key:检测的按键，与```FTC SDK```中手柄按键名称一致，```String```类型
- fn:要运行的函数，建议使用**Lambda表达式**，```Runnnable```类型

### update
每次判断手柄按键时都需要先运行一次，用来更新手柄状态。否则每次循环都会使用上次状态，无法判断按键状态。
#### 示例代码
```java
robot.gamepad1
    .update()//更新状态
    .<other methods>
;
```
{% hint style="danger" %}
本项目还处于早期测试阶段，仅供大家参考。

若用于实际比赛，我们不能保证代码完全可靠运行，也无法对比赛结果负任何责任。
{% endhint %}

### keyPress
当按下key时，执行fn的内容。注意：fn在key按下的期间会**循环运行**。
#### 示例代码
```java
robot.gamepad1
    .update()
    .keyPress("a",AnyFunction())//按住a键
;
```

### keyDown
当按下key时，执行fn的内容。注意：fn在key按下的瞬间只**运行一次**。
#### 示例代码
```java
robot.gamepad1
    .update()
    .keyDown("a",AnyFunction())//按下a键
;
```

### keyUp
当按下key时，执行fn的内容，并进行下一轮判断。注意：fn在key抬起的瞬间只**运行一次**。
#### 示例代码
```java
robot.gamepad1
    .update()
    .keyUp("a",AnyFunction())//抬起a键
;
```

### keyToggle
当按下key时，执行一次fn1的内容；再次按下key，执行一次fn2的内容，并如此循环。
#### 示例代码
```java
robot.gamepad1
    .update()
    .keyToggle("a",AnyFunction1(), Anyfuntion2())//按下a键切换
;
```

**建议在切换的函数中增加遥测的信息显示以确认当前状态**
## 代码示例
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