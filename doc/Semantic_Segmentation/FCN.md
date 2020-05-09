# FCN - Fully Convolutional Networks for Semantic Segmentation

说起语义分割，就不能不提FCN，全称是 Fully Convolutional Networks (全卷积网络)。 我记得FCN应该算是，比较早地将卷积神经网络应用到语义分割任务当中的例子。后期的很多语义分割模型都是在此基础上发展而来的。因此可见FCN在语义分割网络中的重要地位。先来一张论文中关于FCN的网络结构的图吧。

![FCN_Struct](../../img/Semantic_Segmentation/FCN_Structure.png)

不同于之前的深度学习分类网络，FCN没有用全连接层(Fully connected layer)，而是用卷积层进行替代。