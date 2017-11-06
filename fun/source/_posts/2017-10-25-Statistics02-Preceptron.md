---
title: 统计学习方法概论 - 感知机
date: 2017-10-25 14:57:41
categories: Statistics
tags: 
    - ml
---

# 感知机
二类分类的线性分类模型，输入为特征向量，输出为实例的类别。

## 感知机模型

- 输入空间：$\chi \subseteq R^{n}$
- 输出空间：$Y=\{+1,-1\}$
- 映射函数：$f(x)=sign(w\cdot x+b)$其中w和b为感知机模型参数，w叫权值向量，b叫偏置。
- 模型假设空间：定义在特征空间中所有线性分类模型



- 几何解释：$w\cdot x+b=0$对于特征空间$R^n$中的一个超平面S，其中w是超平面的法向量，b是超平面的截距。这个超平面将特征空间分为两个部分。位于两部分的点分为正、负两类。超平面S称为分离超平面。

## 感知机学习策略

### 线性可分性

存在超平面S：$$w\cdot x+b=0$$能将数据集的正实例点和负实例点完全正确的划分到超平面两侧，即对所有$$y_{i}=+1$$的实例i，有$$w\cdot x_{i}+b>0$$，对所有$$y_{i}=-1$$的实例i，有$$w\cdot x_{i}+b<0$$，**则称数据集T为线性可分数据集**。

### 感知机学习策略

目标是找到超平面，即确定w,b参数，为了达到目标，定义损失函数并将损失函数极小化。

损失函数：

- 错误分类点的总数 —— 不是w,b的连续可导函数，不易优化。
- 误分类点到超平面S的总距离 —— 采用

任一点$x_0$到S的距离：
$$
\frac {1}{ \| w \|} \vert w\cdot x_{0}+b\vert
$$
![](/images/2017-10-25-Statistics02-Preceptron-0.jpg)

## 感知机学习算法

现在问题已经转换为求解函数式最优化的问题，最优化的方法是随机梯度下降法。

### 感知机学习算法的原始形式

问题已经转换为以下损失函数极小化问题的解：
$$
\min_{w,b}L(w,b)=-\sum_{x_{i}\subseteq M}y_{i}(w\cdot x_{i}+b)
$$
这里面的变量是w,b。

对w,b求偏导得到梯度：
$$
\nabla_{w}L(w,b)=-\sum_{x_{i}\subseteq M}y_{i}x_{i}
$$

$$
\nabla_{b}L(w,b)=-\sum_{x_{i}\subseteq M}y_{i}
$$

随机选一个误分类点对w,b进行更新：
$$
w\leftarrow w+\eta y_{i}x_{i}
$$

$$
b\leftarrow b+\eta y_{i}
$$

其中$\eta$是步长，在统计学习中称为学习率。

综上：

![](/images/2017-10-25-Statistics02-Preceptron-1.jpg)

### 例子

![](/images/2017-10-25-Statistics02-Preceptron-2.jpg)

1 按照算法2.1求解w,b,学习η=1。

2 取初值$w_{0}=(0,0)^{T}$，这个是初始法向量，如果是三维空间应该是$(0,0,0)^{T}$这里两位就够了。

3 $b_{0}=0$ 

4 $$x_{0}=(3,3)^{T}$$，因为是正分类点，所以$$y_{1}=1$$带入超平面公式：



$$
y_{1}(w_{0}\cdot x_{1}+b_{0})=1((0,0)^{T}\cdot (3,3)^{T}+0)=0
$$

5 这里的$$\cdot$$是内积的意思

$$ x\cdot y=x_{1}y_{1}+x_{2}y_{2}+...+x_{n}y_{n} $$

6 要把所有的正实例和负实例分开，该正实例在分离超平面上，显然不符合要求。所以我们要更新w,b.

7 怎么更新呢，就是w减去他的梯度。（往梯度减少的方向移动）

$$w_{1}=w_{0}+y_{1}x_{1}=0+1(3,3)^{T}=(3,3)^{T}$$

$$b_{1}=b_{0}+y_{1}=1$$

得到线性模型（套公式）

$$w_{1}\cdot x+b_{1}=3x^{(1)}+3x^{(2)}+1$$

**右上角的括号是x的两个维度的意思！**

接着迭代（直到没有误分类点为止！）：

![](/images/2017-10-25-Statistics02-Preceptron-3.jpg)





### 算法的收敛性

定理：当训练数据集线性可分时，感知机学习算法原始形式迭代是收敛的。

### 感知机学习算法的对偶形式

--------------------->>>>>>>>>>没看懂！