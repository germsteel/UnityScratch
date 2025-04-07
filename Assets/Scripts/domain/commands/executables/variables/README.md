# Variables 模块

本模块包含变量操作相关的命令实现，用于设置和修改变量的值。

## 文件说明

- **ChangeVariableByCommand.cs**: 按指定值改变变量的命令
- **SetVariableToCommand.cs**: 设置变量为指定值的命令
- **VariablesDropdownParameter.cs**: 变量下拉参数
- **VariablesDropdownParameterProvider.cs**: 变量下拉参数的提供者

## 类图

```
+----------------+
| ExecutableCommand
+----------------+
        ^
        |
+-------+--------+----------------+
|                |                |
|ChangeVariableByCmd|  SetVariableToCmd
+----------------+----------------+
| + OnEnterAsync()|  | + OnEnterAsync()|
+----------------+  +----------------+
        |                   |
        v                   v
+----------------+
|VariablesDropdownParameter
+----------------+
| + GetValue()   |
+----------------+
```
