# PyTorch 用户手册（Pytorch User Manual）
![pytorch](pytorch-logo-dark.png)

## 用户手册介绍
这是一个开源的关于Pytorch的用户手册，目标是帮助那些希望和使用PyTorch进行深度学习开发和研究的朋友快速入门。

由于笔者水平有限，在写此教程的时候参考了一些网上的资料，在这里对他们表示敬意，文中会在每个引用中附上原文地址，方便大家参考。

用户手册主要包含：
1）Pytorch训练策略以及常见问题；
2）Pytorch训练技巧以及涨点方案；
3）Pytorch搭建自己的网络结构及工程代码；
3）Pytorch部署常见问题及相关工具；

## 版本说明
由于PyTorch版本更迭，教程的版本会与PyTorch版本，保持一致。

## 目录

### 第一章：Pytorch训练策略以及常见问题

### 第二章：Pytorch训练技巧以及涨点方案

### 第三章：Pytorch搭建自己的网络结构及工程代码

### 第四章：Pytorch部署常见问题及相关工具

1. ONNX模型部署

通过修改模型，实现动态输入，链接：https://mmdeploy.readthedocs.io/zh_CN/latest/05-tutorial/02_challenges.html

示例是一个图像超分辨率的例子，其中想实现的是通过外部的变量实现不同倍率的插值方式，但是在 PyTorch 中无论是使用最早的 nn.Upsample，还是后来的 interpolate，PyTorch 里的插值操作最后都会转换成 ONNX 定义的 Resize 操作。也就是说，所谓 PyTorch 转 ONNX，实际上就是把每个 PyTorch 的操作映射成了 ONNX 定义的算子。

因此需要自己生产一个ONNX的Resize算子，让scales成为一个支持外部输入的变量，从而实现模型的动态缩放的输入。具体可以参考上述链接

"""
"""


## License

![](https://i.creativecommons.org/l/by-nc-sa/3.0/88x31.png)

[本作品采用知识共享署名-非商业性使用-相同方式共享 3.0  中国大陆许可协议进行许可](http://creativecommons.org/licenses/by-nc-sa/3.0/cn)
