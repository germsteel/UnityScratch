# Rotate By 模块

本模块包含相对旋转相关的命令实现，用于按相对角度旋转对象。

## 文件说明

- **RotateByVectorCommand.cs**: 按向量相对旋转命令，将对象按指定的角度向量进行旋转

## 类图

```
+----------------+
|BaseRotateCommand|
+----------------+
        ^
        |
+-------+--------+
|RotateByVectorCommand
+----------------+
| + OnEnterAsync()|
| + OnExitAsync() |
+----------------+
```
