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

### 第二章：场景问题以及常见解决方案

### 第三章：Pytorch搭建自己的网络结构及工程代码

### 第四章：Pytorch部署常见问题及相关工具

# 场景问题

大规模商品图像检索任务中常采用的池化方式：GeM pooling，广义均值池 (GeM)计算张量中每个通道的广义均值，增加池化特征图的对比度，并专注于图像的显着特征。

假设是CNN提取后的第k个特征图，是第k个特征图池化后的结果。GeM Pooling可以看作Average Pooling和Max Pooling的延申，

当p=1时，GeM Pooling退化成Average Pooling，当p无穷大时，GeM pooling 等效于Max Pooling.

![image](https://user-images.githubusercontent.com/12441747/160539356-a863389e-68e0-42e1-9071-27a23f5e9575.png)

参考链接：https://amaarora.github.io/2020/08/30/gempool.html

基于池化的向量进行group和SKU-level的多任务分类，分类器采用了CircleSoftmax调整类间间距，并且在每一个分类器之前引入了一个BNNeck[5]的结构。Loss上采用了FocalLoss[6]和CrossEntropy Loss联合训练的方式。

## License

![](https://i.creativecommons.org/l/by-nc-sa/3.0/88x31.png)

[本作品采用知识共享署名-非商业性使用-相同方式共享 3.0  中国大陆许可协议进行许可](http://creativecommons.org/licenses/by-nc-sa/3.0/cn)
