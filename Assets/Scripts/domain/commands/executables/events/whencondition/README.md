# WhenCondition Events 模块

本模块包含条件触发事件相关的命令实现，当满足特定条件时触发事件。

## 文件说明

- **WhenConditionEventCommand.cs**: 条件事件命令，当指定条件满足时触发

## 类图

```
+----------------+
| EventCommand   |
+----------------+
        ^
        |
+-------+--------+
|WhenConditionEventCommand
+----------------+
| + OnEnterAsync()|
+----------------+
```
