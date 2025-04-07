# Move To 模块

本模块包含绝对移动相关的命令实现，用于将对象移动到指定位置。

## 文件说明

- **MoveToVectorCommand.cs**: 移动到指定向量位置的命令，将对象移动到指定的绝对位置

## 类图

```
+----------------+
| BaseMoveCommand|
+----------------+
        ^
        |
+-------+--------+
| MoveToVectorCommand
+----------------+
| + OnEnterAsync()|
| + OnExitAsync() |
+----------------+
```
