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

### 第一章：Backbone

### 第二章：Neck

### 第三章：Head

### 第四章：Loss

## Loss

解决正负样本不均衡问题，从Focal Loss 到 GHM loss

CE的思路：在交叉熵损失前面加上一个参数α，从而去平衡正负样本，但是对难易样本的不平衡没有帮助；

Focal的思路：模型应该主要关心难例样本，将高置信度样本的损失再降低一些，在此基础上再关注平衡样本，从置信度p的角度衰减loss；

GHM的思路：样本中具备离散点，关注难例的问题就是让模型只关注到了这些离散点，另外两个超参数需联合实验，从一定范围置信度p的样本数量的角度衰减loss；

单位梯度模长g部分的样本个数，对于每个样本，把交叉熵CE×该样本梯度密度的倒数即可。


“Gradient Harmonized Single-stage Detector",AAAI2019

![image](https://user-images.githubusercontent.com/12441747/160329733-6609cd6a-ad8d-4655-9219-2d225e8e3290.png)

参考： https://zhuanlan.zhihu.com/p/80594704


## License

![](https://i.creativecommons.org/l/by-nc-sa/3.0/88x31.png)

[本作品采用知识共享署名-非商业性使用-相同方式共享 3.0  中国大陆许可协议进行许可](http://creativecommons.org/licenses/by-nc-sa/3.0/cn)
