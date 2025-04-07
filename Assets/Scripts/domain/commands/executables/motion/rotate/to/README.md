# Rotate To 模块

本模块包含绝对旋转相关的命令实现，用于将对象旋转到指定角度。

## 文件说明

- **RotateToVectorCommand.cs**: 旋转到指定向量角度的命令，将对象旋转到指定的绝对角度

## 类图

```
+----------------+
|BaseRotateCommand|
+----------------+
        ^
        |
+-------+--------+
|RotateToVectorCommand
+----------------+
| + OnEnterAsync()|
| + OnExitAsync() |
+----------------+
```
