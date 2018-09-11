---
title: 数理统计的基本概念
date:  2018/4/22
categories: 数学
mathjax: true
---

# 总体与样本

## 总体    个体    样本

一般将研究对象的全体组成的集合成为**总体**,组成总体的每一个成员成为**个体**.

从总体中挑选一部分个体的过程叫**样本**, 样本所含的个体数称为**样本容量**.

## 抽样方法

抽样要保证对每一个个体"机会均等",即总体中每一个体有同样机会被抽到,谁也不占优.凡是满足这个要求的抽样叫做**随机抽样**.

常用随机抽样方案:

(1)"集团抽样".即先把总体中的全部个体,按某种考虑分成一些大集团,每个大集团内又可分为若干小集团,后者还可以再细分.抽样时,先用随机的方法抽取若干个大集团,再在抽出的每个大集团内分别抽出若干个小集团,$\cdots \cdots$这样下去,最后在最低一级的集团中随机抽出若干个体.这样抽出的全部个体构成所需的样本.

(2)"分层按比例抽样".必须有两个条件:一是分层的标准应合理.这主要是指层与层之间确实有较大差异,而每层内各个个体的差异较小.二是每层所含个体数在总体全部个体数所占的比例要能够比较确切地知道.

# 样本分布和统计量

## 样本分布

样本是按照一定的方法从总体中抽出的一部分个体所组成的集合.样本总所含的个体数称为**样本容量**或**样本大小**.

将$n$个抽象的随机变量$X_1,X_2,\cdots,X_n$称为样本,而把具体的观测数字$(x_1,x_2,\cdots,x_n)$看成该样本的一组取值.

样本$(X_1,X_2,\cdots,X_n)$既然是随机变量,也就有其概率分布.样本的概率分布称为**样本分布**.

作为随机变量的$X_1,X_2,\cdots,X_n$可以认为是相互独立且有相同的分布,每一个$X_i$的分布都与总体$X$有相同的分布.

"随机抽样"的要求保证了样本分量$X_1$与总体$X$同分布的性质,"每次抽取时,总体成分保持不变"的要求保证了样本的各分量$X_1,\cdots,X_n$相互独立且都与总体$X$有相同分布的性质.

统计学中将"每次抽取时,总体的成分保持不变的随机抽样"称为**简单随机抽样**.

由简单随机抽样得到的样本称为**随机样本**.

## 统计量

对样本进行必要的加工和运算处理后得到的结果称为**统计量**.

常用统计量:

1. 样本均值

$$\bar{X}=\frac{1}{n}\sum_{i=1}{n}X_k$$

2. 样本方差

$$S^2=\frac{1}{n-1}\sum_{i=1}^{n}(X_i-\bar{X})^2$$

3. 样本标准差

$$S=\sqrt{S}=\sqrt{\frac{1}{n-1}\sum_{i=1}{n}(X_i-\bar{X})^2}$$

4. 样本$k$阶原点矩

$$A_k=\frac{1}{n}\sum_{i=1}^nX_i^k$$

5. 样本$k$阶中心矩

$$B_k=\frac{1}{n}\sum_{i=1}{n}(X_i-\bar{X})^k$$

6. 从总体$X$中抽取一容量为$n$的样本$X_1,X_2,\cdots,X_n$,设相应的观测值为$x_1,\cdots,x_n$,将观测值按由小到大的次序重新排列为

$$x_{(1)} \le x_{(2)} \le \cdots \le x_{(n)}$$

则称$x_{(1)},\cdots,x_{(n)}$为原始样本观测值$x_1,\cdots,x_n$的**次序样本观测值**.$x_{(1)},\cdots,x_{(n)}$由$x_1,\cdots,x_n$确定,$x_1,\cdots,x_n$的值有一定随机性,导致$x_{(1)},\cdots,x_{(n)}$的值也有一定随机性.为此,将次序样本观测值$x_{(1)},\cdots,x_{(n)}$看成(想象成)某$n$个随机变量$X_{(1)},\cdots,X_{(n)}$(其分布可能与$X_1,\cdots,X_n)$截然不同)的观测值,如此定义的$n$为随机变量$(X_{(1)},\cdots,X_{(n)})$被称为原始样本$X_1,\cdots,X_n)$的**次序统计量**.

7. 样本中位数

$$\tilde{X}=\begin{cases} X_(k+1) & \text{if} \quad n=2k+1 \\ \frac{1}{2}(X_{(k)} + X_{(k+1)}) & \text{if} \quad n=2k \end{cases}$$

8. 样本极差

$$R=X_{(n)}-X_{(1)}$$

统计量的实质在于:统计量只依赖与样本$X_1,\cdots,X_n$,而不涉及任何其他未知的量,即它是样本的已知函数$g(X_1,\cdots,X_n)$,且不能含有任何未知参数.

## 统计量的分布

1. $\chi^2$分布

设$X_1,\cdots,X_n$相互独立且都服从$N(0,1)$分布,它们的平方和

$$\chi^2 \stackrel{def} = sX_1^2+ \cdots + X_n^2$$

的分布称为自由度为$n$的$\chi^2$分布,记为$\chi^2 \sim \chi(n)$.

其概率密度

$$f(y)=\begin{cases} \frac{1}{2^{\frac{n}{2}}\Gamma(\frac{n}{2})}y^{\frac{n}{2}-1} e^{-\frac{y}{2}}, & y \ge 0 \\ 0, & y < 0 \end{cases}$$

其中$\Gamma(z)=\int_0^{\infty}u^{z-1}e^{-u}du,(z\ge 0)$.

对任意给定的正数$\alpha(0<\alpha<0)$,称满足条件

$$\int_{\chi_\alpha^2(n)}^{\infty}f(y)dy=\alpha$$

的点$\chi_\alpha^2(n)$为$\chi^2(n)$的上$\alpha$分位点.

$\chi_\alpha^2(n)$的概率意义是:服从$\chi_\alpha^2(n)$分布的随机变量$\chi^2$,取值大于$\chi_\alpha^2(n)$的概率正好等于$\alpha$即

$$P\{\chi^2 > \chi_\alpha^2(n)\}=\alpha$$

若$\chi_1^2 \sim \chi^2(n_1), \chi_2^2 \sim \chi^2(n_2)$,且$\chi_1^2$与$\chi_2^2$独立,则

$$\chi_1^2+\chi_2^2=\chi^2(n_1+n_2)$$

2. $t$分布

设$X\sim N(0,1), Y\sim \chi^2(n)$,且$X,Y$相互独立,则随机变量

$$t\stackrel{def} =  \frac{X}{\sqrt{Y/n}}$$

的分布称为自由度$n$的$t$分布,记为$t \sim t(n)$.

$t(n)$分布的概率密度为

$$f(x)=\frac{\Gamma(\frac{n+1}{2})}{\sqrt{n\pi}\Gamma(\frac{n}{2})}(1+\frac{t^2}{n})^{-\frac{n+1}{2}}, \qquad -\infty < t < +\infty$$

其中$\Gamma(z)=\int_0^{\infty}u^{z-1}e^{-u}du,(z\ge 0)$.

3. $F$分布

设$U\sim \chi^2(n_1), V\sim \chi^2(n_2)$,且$U,V$相互独立,则随机变量

$$F \stackrel{def} =  \frac{U/n_1}{V/n_2}$$

的分布称为自由度$(n_1,n_2)$的$F$分布,记为$F\sim F(n_1,n_2)$. 其中$n_1,n_2$分别称为第一,第二自由度.

$F(n_1,n_2)$分布的概率密度为

$$f(y)=\begin{cases} \frac{\Gamma(\frac{n_1+n_2}{2})}{\Gamma(\frac{n_1)}{2}\Gamma(\frac{n_2)}{2}} (\frac{n_1}{n_2})(\frac{n_1}{n_2}y)^{\frac{n_1}{2}-1}(1+\frac{n_1}{n_2}y)^{-\frac{n_1+n_2}{2}}, & y \ge 0 \\ 0 & y < 0 \end{cases}$$

$F(n_1,n_2)$分布的上$\alpha$分为点定义为满足条件

$$\int_{F_\alpha(n_1,n_2)}^{\infty}f(y)dy=\alpha$$

的点$F_\alpha(n_1,n_2)$. 并且

$$F_{1-\alpha}(n_2,n_2)=\frac{1}{F_\alpha(n_1,n_2)}$$

## 与正态总体统计量有关的分布

1. 若$X$服从一元正态分布$N(\mu, \sigma^2)$,则$X$的线性函数

$$aX+b \sim N(a\mu+b, a^2 \sigma^2)$$

特别

$$\frac{X-\mu}{\sigma} \sim N(0,1)$$

2. 若$X \sim N(\mu_1, \sigma_1^2), Y \sim N(\mu_2, \sigma_2^2)$,且$X$与$Y$相互独立,则

$$X \pm Y \sim N(\mu_1 + \mu_2, \sigma_1^2 + \sigma_2^2)$$

3. 如果随机变量$\mathbf{X}$服从均值向量为$\mathbf{\mu}$,协方差矩阵为$\mathbf{\Sigma}$的$n$元正态分布$N(\mathbf{\mu, \Sigma}),\mathbf{A}$是$m$行$n$列的常数矩阵,则$m$维随机向量

$$\mathbf{AX} \sim N(\mathbf{A\mu,A\Sigma A'})$$

4. 显然$\frac{X_1-\mu}{\sigma},\frac{X_2-\mu}{\sigma},\cdots,\frac{X_n-\mu}{\sigma}$独立同$N(0,1)$分布,由$\chi^2$分布的定义可知它们的平方和

$$\frac{1}{\sigma^2} \sum_{i=1}^{n}(X_1-\mu)^2 \sim \chi^2(n)$$

5. 由独立正态变量的线性运算性质得

$$\sum_{i=1}^nX_i \sim N(n\mu, n\sigma^2)$$

所以

$$\bar{X}=\frac{\displaystyle \sum_{i=1}^nX_i}{n} \sim N(\mu, \frac{\sigma^2}{n})$$

标准化得

$$\frac{\bar{X} - \mu}{\sigma / \sqrt{n}} \sim N(0,1)$$

6. 

$$\frac{1}{\sigma^2}\sum_{i=1}{n}(X_i-\bar{X})^2 \sim \chi^2(n-1)$$

亦即

$$\frac{(n-1)S^2}{\sigma^2} \sim \chi^2(n-1)$$

7. $\frac{\sqrt{n}{\bar{X}-\mu}}{\sigma}$与$\frac{n-1)S^2}{\sigma^2}$相互独立.

8. 

$$\frac{\sqrt{n}(\bar{x}-\mu)}{S} = \frac{\frac{\sqrt{n}(\bar{x}-\mu)}{\sigma}}{\sqrt{\frac{(n-1)S^2}{(n-1)\sigma^2}}} \sim t(n-1)$$

9.

$$\frac{(\bar{X}-\bar{Y})-(\mu_1-\mu_2)}{\sqrt{\frac{\sigma_1^2}{n_1} + \frac{\sigma_2^2}{n_2}}} \sim N(0,1)$$
