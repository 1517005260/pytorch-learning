# 神经网络理论基础 NN

## 神经网络层级结构

### 概念
神经网络是一种模仿生物神经系统的计算模型，用于解决分类、回归、生成等机器学习问题。神经网络的层级结构包括输入层、隐藏层和输出层，每一层都由若干个神经元（节点）组成，每个节点又叫做感知机模型。

#### 三个基本概念：
- 输入层（网络第一层，用于输入特征和数据） 
- 隐藏层 ：参数可以人为手动调整，用于处理数据
- 输出层（输出计算结果）

#### 图例
![神经网络层级结构](/NeuralNetwork/image/1.png)

==> <b>深度学习模型</b> ~ 复杂的、有很多的隐藏层的神经网络

##### 基于神经网络有很多变体算法
1. CNN 卷积神经网络  用于处理图像
2. RNN 循环神经网络  用于处理文本
3. GAN 生成对抗网络  图片生成
4. Auto-Encoder 
5. Transformer
6. GNN 图神经网络
…………

## 神经网络是如何对数据做特征提取的
![对于一个感知机的分析](/NeuralNetwork/image/2.png)

### 分析一个感知机（节点）的计算方法
- xi ：输入数据
- wi ：权重
- b ：偏移量、偏置值bias
- y : 输出

<b>参数：wi,b</b>

- 在神经网络刚开始训练之初，参数是随机生成的。随着网络的训练，参数会自我更新，慢慢拥有自我意义

==> <i>节点对输入数据xi的处理就是神经网络算法的核心思想</i>
即：
$$
y = \sum_{i=1}^{n} x_{i} \times w_i + b
$$

#### 一个通俗的例子
类比 计量经济学的回归：<br>
假设：一个女孩要判断一个男孩适不适合自己，那么可以对他进行打分：
$$
score = 身高 \times 0.5 + 颜值 \times 0.8 + 财富 \times 1
$$
score就是女孩根据男孩的各种特征，进行的一个打分情况<br>
那么我们可以发现在这个打分过程（感知机模型）中，财富的占比比较高，说明这次的模型偏好财富值<br>
拿到这个分数之后，可以去和阈值（比如60分）做比较，男孩高于60分就进入女话的选择范围

##### 有关b
偏移量，在本例中可以解释为女孩的眼光<br>
举例：如果`b = -10` 那么说明女孩的眼光比较高。如果上例中最后的`score`算出来是65分，那么在加上这个偏移量`b`，导致最后的`score`为55分，小于60分，于是女孩排除了这个男孩<br>
而在具体的感知机模型里，所有的参数都是从数据中学习得到的。

## 神经网络模型pytorch api
![图](/NeuralNetwork/image/1.png)

基于上个例子，我们可以用如下api：
``` python
CLASS torch.nn.Linear(in_features, out_features, bias=Ture, device=None, dtype=None)
```
其中，输入数据个数 = `in_features` = 7<br>
输出结果个数 = 神经网络节点个数 = `out_features` = 4 （去除省略号）<br>
是否启用偏移量计算 = `bias=Ture`<br>
`device=None` = 运行环境：GPU or CPU<br>
`dtype=None` = 当前计算的数据类型，官方推荐FLOAT32