# Move By 模块

本模块包含相对移动相关的命令实现，用于按相对位置移动对象。

## 文件说明

- **MoveByVectorCommand.cs**: 按向量相对移动命令，将对象按指定的向量进行移动

## 类图

```
+----------------+
| BaseMoveCommand|
+----------------+
        ^
        |
+-------+--------+
| MoveByVectorCommand
+----------------+
| + OnEnterAsync()|
| + OnExitAsync() |
+----------------+
```
