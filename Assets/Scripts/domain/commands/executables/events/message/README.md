# Message Events 模块

本模块包含消息事件相关的命令实现，用于对象间的消息通信。

## 文件说明

- **BroadcastMessageEventCommand.cs**: 广播消息事件命令，向所有对象发送消息
- **Message.cs**: 消息类，定义消息的结构
- **MessageEventArgs.cs**: 消息事件参数
- **MessageHandler.cs**: 消息处理器
- **MessagesDropdownParameter.cs**: 消息下拉参数
- **MessagesDropdownParameterProvider.cs**: 消息下拉参数的提供者
- **MessagesManager.cs**: 消息管理器，负责消息的注册和分发
- **ReceiveMessageEventCommand.cs**: 接收消息事件命令，当收到指定消息时触发

## 类图

```
+----------------+     +----------------+
| EventCommand   |     | MessagesManager|
+----------------+     +----------------+
        ^              | + Instance     |
        |              | + Register()   |
+-------+--------+     | + Broadcast() |
|BroadcastMessageCmd|  +----------------+
+----------------+            |
| + OnEnterAsync()|           |
+----------------+     +------+-------+
        ^              | Message      |
        |              +-------------+
+-------+--------+     | + Key       |
|ReceiveMessageCmd|    +-------------+
+----------------+
| + OnEnterAsync()|
+----------------+
```
