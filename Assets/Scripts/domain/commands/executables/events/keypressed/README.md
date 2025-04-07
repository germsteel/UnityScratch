# KeyPressed Events 模块

本模块包含按键事件相关的命令实现，用于响应键盘按键事件。

## 文件说明

- **KeyPressedEventCommand.cs**: 按键事件命令，当指定按键被按下时触发
- **KeyPressedEventListener.cs**: 按键事件监听器，负责检测和分发按键事件
- **ValidKeysDropdownParameter.cs**: 有效按键的下拉参数
- **ValidKeysDropdownParameterProvider.cs**: 有效按键下拉参数的提供者

## 类图

```
+----------------+     +----------------+
| EventCommand   |     | MonoBehaviour  |
+----------------+     +----------------+
        ^                      ^
        |                      |
+-------+--------+    +--------+-------+
|KeyPressedEventCommand| |KeyPressedEventListener
+----------------+    +----------------+
| + OnEnterAsync()|   | + Update()     |
+----------------+    +----------------+
        |
        v
+----------------+
|ValidKeysDropdownParameter
+----------------+
| + GetValue()   |
+----------------+
```
