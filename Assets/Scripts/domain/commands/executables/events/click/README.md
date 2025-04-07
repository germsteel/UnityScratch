# Click Events 模块

本模块包含点击事件相关的命令实现，用于响应对象的点击事件。

## 文件说明

- **ClickEventCommand.cs**: 点击事件命令，当对象被点击时触发
- **ClickEventListener.cs**: 点击事件监听器，负责检测和分发点击事件

## 类图

```
+----------------+     +----------------+
| EventCommand   |     | MonoBehaviour  |
+----------------+     +----------------+
        ^                      ^
        |                      |
+-------+--------+    +--------+-------+
| ClickEventCommand|   | ClickEventListener
+----------------+    +----------------+
| + OnEnterAsync()|   | + OnMouseDown()|
+----------------+    +----------------+
```
