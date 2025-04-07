# Events 模块

本模块包含事件相关的命令实现，用于响应各种事件触发。

## 文件说明

- **EventCommand.cs**: 事件命令的基类

## 子模块

- **click**: 点击事件相关命令
- **keypressed**: 按键事件相关命令
- **message**: 消息事件相关命令
- **whencondition**: 条件触发事件相关命令

## 类图

```
+----------------+
| ExecutableCommand
+----------------+
        ^
        |
+-------+--------+
|  EventCommand  |
+----------------+
        ^
        |
+-------+--------+
|  具体事件命令   |
+----------------+
| ClickEvent     |
| KeyPressedEvent|
| MessageEvent   |
+----------------+
```
