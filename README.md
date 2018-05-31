# neural-style-master


实际操作是通过不带全连接层的vgg网络分别抽取内容图、画风图以及生成图（就是最后你画的“名画”）的特征图，然后分别用内容特征和生成特征图计算内容损失，用画风图和生成图计算风格损失，将两个损失合起来，作为总体损失，用总体损失来计算生成图的梯度然后更新生成图。生成图最初初始化为白噪声图。vgg用imagenet预训练模型。


根据生成图的内容与目标内容的差异来“画”（优化）内容；用生成图与目标画风的差异来“画”（优化）风格。（下面这句为个人理解）这样一来，上面框图中最上面的网络和最下面的网络实际只跑一次，但中间网络要跑N次，但这N次跑前向和后向，后向不会优化网络参数，只会优化生成图。


特征图可以选择vgg 5个卷积模块中任何一个模块的仁义卷积层的输出，实际画风提取了多个卷积层的输出。内容直接用特征图表示；画风采用每个特征图自己与自己的格拉姆矩阵表示，通常将多个卷积层提取的多个特征图作格拉姆矩阵后叠加。



实际操作：
1.图像预处理（内容图、画风图）、生成图占位符定义
2.预训练模型加载
3.三张图跑网络
4.内容损失计算
5.格拉姆矩阵计算
6.风格损失计算
7.损失和梯度汇总
8.设置迭代计算图
10.选择生成图优化方法
11.开始迭代

样式图:
![](https://github.com/ttanzhiqiang/neural-style-master/blob/master/v2-fc8c6a5a840ea83f5e5d3241707d08bc_r.jpg)

原图:
![](https://github.com/ttanzhiqiang/neural-style-master/blob/master/2-content.jpg)
风格图:
![](https://github.com/ttanzhiqiang/neural-style-master/blob/master/shipwreck.jpg)
输出图:
![](https://github.com/ttanzhiqiang/neural-style-master/blob/master/y-output.jpg)
