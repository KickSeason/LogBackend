# neo插件简介
通用插件类型：LogPlugin, PersistencePlugin, PolicyPlugin, RpcPlugin
自定义插件类型
## 通用plugin
### LogPlugin
实现Log方法，在输出共识log时也会调用此方法，得到日志内容
### PersistencePlugin
实现onPersist方法， 并在接收到新区块时调用，得到区块快照
### PolicyPlugin
实现FilterForMemoryPool方法，可以过滤写入memorypool的交易
实现FilterForBlock可以过滤写入区块的交易，这个只会在作为议长有效
### RpcPlugin
实现OnProcess方法，neo收到rpc时会调用此方法
## 自定义插件
### Akka.Actor
使用akka的tell或者ask调用neo内部的功能， 或者继承Actor并注册到neo内部模块中，需要neo内部修改和支持
### 使用neo的命名空间
可以直接使用neo的命名空间
## 结论
使用akka框架和neo的命名空间可以使用neo的功能，但是目前唯一的问题是插件不能与用户直接交互。

## 与neo-python对比
neo-cli与neo-python差异主要在智能合约开发方面。
neo-python可以编译，测试 python语言的智能合约，部署.avm格式智能合约。
目前neo-cli没有智能合约开发相关的东西。
## neo-cli实现测试和部署智能合约
首先，插件里运行运行合约是没有问题的，关键是neo-cli里命令可以操作插件。
需要修改neo-cli可以执行指定插件。
修改neo中插件类支持neo-cli调用插件。
上述改动只是，是neo-cli支持在neo-cli中可以使用插件注册的命令，改动一次之后不需要再修改。
之后，编写响应插件即可在neo-cli命令中使用。

