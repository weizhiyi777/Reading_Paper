# FCN - Fully Convolutional Networks for Semantic Segmentation

说起语义分割，就不能不提FCN，全称是 **Fully Convolutional Networks (全卷积网络)**。 
我记得,FCN应该算是比较早地将**卷积神经网络**应用到**语义分割**任务当中的例子。后期的很多语义分割模型都是在此基础上发展而来的，因此可见FCN在语义分割网络中的重要地位。先来一张论文中关于FCN的网络结构的图吧。

![FCN_Struct](../../img/Semantic_Segmentation/FCN_Structure.png)

FCN网络是第一个能够实现端到端训练的全卷积神经网络。
不同于之前的深度学习分类网络，FCN没有用全连接层(Fully connected layer)，而是用卷积层(Convoluational layer)进行替代。
这样可以带来一个明显的好处：理论上可以接受**任意尺寸**的输入图像，并且输出相对应尺寸的特征图。

我们首先来简单分析下这张网络结构图想要表达的思想。从左向右是前向传播过程，从右向左是反向传播过程。
在前向传播过程中，输入网络的图片，经过了一层一层的卷积层(->96->256->...->4096->21->)。如果其中包含了下采样操作，那么在这个过程中，特征图的尺寸会不断缩小。最后，再经过 `upsampling` 的操作(后面会详细介绍)，可以将特征图生成逐像素(pixelwise)的分类结果。
在反向传播的过程中，我们将我们的预测结果(prediction)与真实值(ground truth)进行对比，计算损失，并根据梯度信息进行网络参数的更新。
和分类网络不同，FCN网络将全连接层替换为卷积层，然后还增加了生成逐像素预测结果(pixelwise prediction)的过程。逐像素预测结果正好可以与真值计算损失(loss)，因此可以实现端到端的训练。

### 全局特征 & 局部特征

我比较喜欢论文中的这样一句话：

> Global information resolves what while local information resolves where.

这句话其实点出了深度学习网络中的一些特征分布的特点：

* 全局特征(高维特征)可以更好地描述整体的语义情况，例如类别信息；
* 局部特征(浅层特征)可以更好地描述细节信息，比如位置、纹理、颜色等等。

一般来说，针对分类任务的深度学习模型对输入的图片进行一层一层地信息提取，先提取浅层特征，然后再提取高维特征，最后告诉使用者图片的类别。这样的过程就有点像总结和归纳。而针对语义分割模型而言，如果要实现逐像素的分类，那么就必须要同时解决what(分类)和where(分割)的问题。因此，语义分割模型往往需要融合局部特征和全局特征，并给出最后的答案。

文中还对感受野(receptive fields)做出了一定的解释：因为卷积操作的原因，前一层特征图的像素位置(x<sub>ij</sub>)与后一层的特征图的像素位置(y<sub>ij</sub>)存在一定的对应关系，这种对应关系就反映了感受野这个特点。

此外，文中还针对全连接层和卷积层提出了自己的看法：全连接层可以看作是一种特殊的卷积层，其卷积核的输入为整个特征图。

### 关于上采样(Unsampling)

未完待续…………

------------------
### 参考文献

1. Fully Convolutional Networks for Semantic Segmentation : https://arxiv.org/abs/1411.4038