---
title: 梯度下降
date:  2018/4/24
categories: 机器学习
mathjax: true
---

梯度下降就是在函数当前点梯度(偏导)的反方向的规定步长进行迭代,直至收敛(即到达局部最小值).

批量梯度下降

假设有损失函数

$$J(\theta)=\frac{1}{2}\sum_{i=1}^{m}(h_\theta(x^{(i)})-y^{(i)})^2$$

其中$h_\theta(x)=\theta_0 + \theta_1x_1 + \theta_2x_2 + \cdots + \theta_nx_n$.

那么

$$\theta_j:=\theta_j - \alpha \frac{\partial}{\partial \theta_j}J(\theta)$$

$$\begin{aligned} \frac{\partial}{\partial \theta_j}J(\theta) = \sum_{i=1}^{m}(h_\theta(x^{(i)})-y^{(i)})x_j^{(i)} \end{aligned}$$

所以

$$\theta_j:=\theta_j + \sum_{i=1}^{m}( y^{(i)} - h_\theta(x^{(i)}))x_j^{(i)}$$

以上公示就是批量梯度下降,每一次迭代$\theta_j$时,都需要完全遍历整个输入集合.

随机梯度下降

假设只有一个输入样本,则

$$\theta_j:=\theta_j + ( y - h_\theta(x)x_j$$

以上就是随机梯度下降的公式.即每次更新$\theta_j$只用一个样本.
