---
title: 概率论总结
date:  2018/4/19
categories: 数学
mathjax: true
---

# 基本概念

## 古典概型

### 古典改型的特点:

(1) 试验的样本空间中的元素个数只有有限个,不妨设为n个,记为$e_1,e_2,...,e_n$;
(2) 每个基本事件$\{e\}$出现的可能性相等,即有

$$P(\{e_1\})=P(\{e_2\})=...=P(\{e_n\})$$

### 古典概型类型

#### 随机取数问题

(1) 有放回地随机取数: 若从$n$个相异的数字中有放回地取$m$个, 则试验样本空间的基本事件总数可按$n$个不同数字中取$m$个的重复排列计算,由乘法原理知为$n*n*... *n=n^m$

(2) 无放回地随机取数: 若取出的数不还原,则从n个不同的数中任取$m$个试验样本空间所含基本事件总数要根据取数是计序或不计序,按不重复的排列或组合公式计算,即基本事件总数为:

(a) 计序时为$A_n^m=n(n-1)...(n-m+1)$

(b) 不计序时为$C_n^m= \left( \begin{matrix} n \\ m \end{matrix} \right)=\frac{n!}{m!(n-m)!}$

#### 抽球问题

从$n$个球中抽取$m$个:

(1)有放回

(a)计序: $n^m$

(b)不计序: $C_{n+m-1}^m$, 相当于在$n+m-1$个球中无放回抽取$m$个球

(2)无放回

(a)计序: $A_n^m$

(b)不计序: $C_n^m$

#### 分房问题

设有$n$个人,每个人都等可能的被分配到$N$个房间中的任意一间中去住$(n\le N)$, 且每个房间可容纳的人数不限.

#### 配对问题

## 几何概型

(1) 每次试验的可能有无限多个,且全部可能结果的集合可用一个有度量(如长,面积,体积等)的几何区域来表示.

(2) 每次试验中每个可能的出现是等可能的.

## 条件概率

设$A, B$为两事件,且$P(A) \gt 0$, 称

$$P(B|A)=\frac{P(AB)}{P(A)}$$

为在事件$A$发生条件下事件$B$发生的概率.

全概率公式

设试验$E$的样本空间$S$, $A$为$E$的事件, $B_1,B_2,...,B_n$为$S$的一个划分,且$P(B_i)\gt 0(i=1,2,...,n)$, 则

$$P(A)=P(B_1)P(A|B_1)+P(B_2)P(A|B_2)+...+P(B_n)P(A|B_n)$$

贝叶斯公式

设试验$E$的样本空间$S$, $A$为$E$的事件, $B_1,B_2,...,B_n$为$S$的一个划分,且$P(A)>0, P(B_i)\gt 0(i=1,2,...,n)$, 则

$$P(B_i|A)=\frac{P(B_i)P(A|B_i)}{\sum_{j=1}^nP(B_j)P(A|B_js)}$$

## 事件独立

设$A$,$B$是两事件,如果具有等式

$$P(AB)=P(A)P(B)$$

则称$A$,$B$为相互独立事件.

# 随机变量

## 概念

设$E$是随机试验, 其样本空间$S=\{e\}$. 如果对应每一个$e \in S$, 均有一个实数$X(e)$与之对应, 这样一个定义在样本空间$S$上的单值实数$X=X(e)$, 称为随机变量.

设$X$是一个随机变量, $x$是任意实数, 函数

$$F(s)=P\{X \le x\}$$

称为$X$的分布函数.

分布函数的基本性质:

(1) $F(x)$是一个不减函数.

(2) $0 \le F(x) \le 1$ 且 $F(-\infty)= \lim_{x \rightarrow -\infty}F(x) = 0 \quad F(+\infty)= \lim_{x \rightarrow +\infty}F(x) = 1$

## 离散型随机变量

若随机变量$X$的可能取值仅有有限个或可列多个,则称此随机变量为离散型随机变量.

### 常见分布

#### 单点分布

设随机变量$X$取一个常数值$C$的概率为1, 即$P\{X=C\}=1$, 则称$X$服从单点分布或退化分布.

#### (0-1)分布(两点分布)

设随机变量$X$只可能取0和1两个值,它的分布律是

$$P\{X=k\}=p^k(1-p)^{1-k} \qquad k=0,1; 0 < p < 1$$

则称$X$服从(0-1)分布.

#### 等可能分布(离散型均匀分布)

如果随机变量$X$可以取$n$个不同的值$x_1<x_2<...<x_n$, 且取每个$x_k$值的概率相等, 即

$$P\{X=x_k\}=\frac {1}{n}$$

则称$X$服从等可能或称离散型均匀分布.

#### 二项分布

如果随机变量$X$取值为$0,1,2,...,n$的概率为

$$P\{X=k\}= \left( \begin{matrix}  n \\ k \end{matrix} \right) p^k (1-p)^{n-k}$$

则称$X$服从参数为$n,p$的二项分布, 记为$X \sim B(n,p)$

设试验$E$的可能结果只有两个,即$A$或$\bar{A}$, 且$P(A)=p, P(\bar{A})=1-p=q(0<p<1)$, 若将此试验$E$独立地重复$n$次,则称这一串重复的独立试验为$n$重贝努力(Bernoulli)试验,或称$n$重贝努力概型.

#### 泊松分布

如果随机变量X的可能取值为$0,1,2,...$取各值的概率为

$$P\{X=k\}=\frac{\lambda ^k e^{-\lambda}}{k!}$$

其中$\lambda>0$为常数,则称$X$服从参数为$\lambda$的泊松分布,记为$X \sim P(\lambda)$.

泊松逼近定理

设$\lambda > 0$是一常数, $n$是任意正整数, 设$np_n=\lambda$, 则对于任一固定的非负整数$k$, 有

$$\lim_{n\rightarrow \infty} \left( \begin{matrix}n \\ p \end{matrix} \right) (1-p_n)^{n-k} = \frac{\lambda ^k e^{-\lambda}}{k!}$$

#### 几何分布

如果随机变量$X$可能取值为$1,2,..$的概率为

$$P\{X=k\}=pq^{k-1} \qquad k=1,2,..., \quad 0 < p < 1, \quad q=1-p$$

则称$X$服从参数为$p$的几何分布,记为$X \sim Ge(p)$.

几何分布的数学描述:

若进行一系列重复的独立试验,每次试验中某事件$A$发生的概率为$p$,即$p=P(A)$, 令$X$表示事件$A$首次发送时试验的总次数,则此$X$服从参数为$p$的几何分布.

#### 帕斯卡分布(负二项分布)

如果随机变量$X$的概率分布为

$$P\{X=k\}=\left( \begin{matrix} k-1 \\ r-1 \end{matrix} \right) p^r q^{k-r} $$

$$k=r,r+1,r+2,...,r \ge 1, \quad 0 < p < 1, \quad q = 1-p$$

则称$X$服从参数为$p,r$的帕斯卡分布或负二项分布.

帕斯卡分布的数学描述;

若进行一系列重复的独立试验, 每次试验中某事件$A$发生的概率为$p$发生的概率为$p$, 即$p=P(A)$.
令$X$表示在事件$A$恰发生$r$次时试验的总次数,则此$X$服从参数为$p,r$的帕斯卡分布.

#### 超几何分布

如果随机变量$X$的概率分布为

$$P\{X=k\}=\frac{\left( \begin{matrix} M \\ k \end{matrix} \right) \left( \begin{matrix} N-M \\ n-k \end{matrix} \right) }{\left( \begin{matrix} N \\ n \end{matrix} \right)}$$

则称$X$服从参数为$n,M,N$的超几何分布.

超几何分布的数学描述:

设一代中总有$N$个产品,其中有$M$个次品,现从中任取$n$个产品,令$X$为$n$个产品中的次品的个数,则此$X$服从参数为$n,M,N$的超几何分布.

定理:

设$p(0<p<1)$为一常数,当$N \rightarrow \infty$时, $\lim \frac{M}{N} = p$, 则对固定的非负整数$n(n\le M)$, 任一固定的非负整数$k=0,1,2,...,n$ 有

$$\lim_{N \rightarrow \infty} \frac {\left( \begin{matrix} M \\ k \end{matrix} \right) \left( \begin{matrix} N-M \\ n-k \end{matrix} \right)}{\left( \begin{matrix} N \\ n \end{matrix} \right)} = \left( \begin{matrix} n \\ k \end{matrix} \right)p^k(1-p)^{n-k}$$

## 连续型随机变量

### 概念

如果对于随机变量$X$的分布函数$F(x)$, 存在非负函数$f(x)$, 使对于任意实数$x$均有

$$F(x)=\int^x_{-\infty} f(t)dt $$

则称$X$为连续型随机变量, 其中函数$f(x)$称为$X$的概率密度函数,简称概率密度.

概率密度$f(x)$具有以下性质:

(1) $f(x) \ge 0$

(2) $\int_{- \infty}^{+ \infty}f(x)dx=1$

(3) $P\{x_1 < X \le x_2\} = F(x_2) - F(x_1) = \int_{x_1}^{x_2}dx \qquad (x_1 \le x_2$)

(4) 若$f(x)$在点$x$处连续, 则有$F^{'}(x) = f(x)$

对于连续型随机变量$X$来说,$X$取任一固定值$a$的概率为0, 故连续型随机变量概率与区间开闭无关:

$$P\{a \le x \le b\} = P\{a \le x < b\} = P\{a < x \le b\} = P\{a < x < b\}$$

### 连续型随机变量的分布

#### 均匀分布

若随机变量$X$具有概率密度

$$f(x)=\begin{cases} & \frac{1}{b-a} \quad & a < x < b \\ & 1 \quad & x \ge b, x \le a \end{cases}$$

s则称$X$服从$(a,b)$上的均匀分布, 记作$X \sim U(a,b)$. 当参数$a=0, b=1$时, $U(a,b)$成为标准分布.

容易得到$X$的分布函数为

$$f(x)=\begin{cases} 0 & x<a \\ \frac{x-a}{b-a} & a \le x < b \\ 1 & x \ge b \end{cases}$$

#### 指数分布

若随机变量$X$具有概率密度

$$f(x)=\begin{cases} \alpha e^{-\alpha x} & x>0 \\ 0 & x \le 0 \end{cases}$$

其中参数$\alpha > 0$, 则称随机变量$X$服从参数为$\alpha$的指数分布, 记为$X \sim Z(\alpha)$.

其分布函数为

$$F(x)=\begin{cases} 1-e^{-\alpha x} & x > 0 \\ 0 & x \le 0 \end{cases}$$

#### 正态分布

若随机变量$X$具有概率密度

$$f(x)=\frac{1}{\sqrt{2 \pi \sigma}} e^{-\frac{(x-\mu)^2}{2 \sigma^2}}$$

则称$X$服从参数为$\mu$和$\sigma^2(\sigma > 0)$的正态分布,记作$X \sim N(\mu, \sigma^2)$, 此时称$X$为正态变量.

$X$的分布函数为

$$F(x)=\int _{-\infty}^x \frac{1}{\sqrt{2 \pi \sigma}} e^{-\frac{(t-\mu)^2}{2 \sigma^2}} dt \qquad -\infty < x < +\infty$$

当$\mu =0, \sigma = 1$时, $X \sim N(0,1)$, 称$X$服从标准正态分布,称$X$为标准正态变量. 它的概率密度和分布函数分布标记为

$$\varphi(x)=\frac{1}{\sqrt{2\pi}}e^{-\frac{x^2}{2}} \qquad -\infty<x<+\infty $$

$$\Phi(x)=\frac{1}{\sqrt{2\pi}}\int_{-\infty}^{x}e^{-\frac{t^2}{2}}dt \qquad -\infty<x<+\infty $$

若$X \sim N(\mu, \sigma^2)$, 其分布函数为$F(x)$, 则标准化变量

$$Z=\frac{X-\mu}{\sigma} \sim N(0,1)$$

且

$$F(x)=\Phi(\frac{x-\mu}{\sigma})$$

设随机变量$X$的分布函数$F(x)$,对于任一正数$\alpha(0<\alpha<1)$, 若$X$大于等于某实数$z_\alpha$, 即

$$1-F(z_\alpha)=P\{X \ge z_\alpha\} = \alpha \qquad 0 < \alpha < 1$$

则称此实数$z_\alpha$为分布$F(x)$的上$\alpha$分为点.

## 随机变量的函数的分布

### 离散型随机变量的函数的分布

离散型随机变量的函数$Y=g(X)$仍是离散型随机变量.计算离散型随机变量的函数的分布律,首先找出它的一切可能值,然后计算它取各个值的概率.

### 连续型随机变量的函数的分布

如果$X$是连续型随机变量,函数$g(x)$是连续函数,这时$Y=g(X)$也是一个连续型随机变量.

设连续型随机变量$X$的概率密度为$f_X(s)$, 当$a<x<b$时, $f_X(x)>0;y=g(x)$处处可导, 且恒有$g'(x)>0$(或$g'(x)<0$),则随机变量$X$的函数$Y=g(X)$的概率密度为

$$f_Y(y)=\begin{cases} f_X(h(y))|h'(y)| & c<y<d \\ 0 & y\ge d, y < c \end{cases}$$

其中$x=h(y)$为$y=g(x)$的反函数, $c=min\{g(a), g(b)\}, d=max\{g(a),g(b)\}$

设随机变量$X \sim N(\mu, \sigma^2)$, $X$的线性函数$Y=aX+b(a\neq 0)$也服从正态分布.

# 多维随机变量

## 二维随机变量

设$E$为一个随机试验,它的样本空间为$S=\{e\}$, 并设$X=X(e)$和$Y=Y(e)$是定义在$S$上的随机变量,由它们两个构成的联合变量$(X,Y)$,称为二维随机变量或二维随机向量.

设$(X,Y)$是定义在样本空间$S=\{e\}$上的二维随机变量, 对于任意实数$x,y$, 二元函数

$$F(x,y)=P\{(X\le x) \cap (Y\le y)\} \triangleq P\{X\le x, Y\le y\}$$

称为二维随机变量$(X,Y)$的分布函数, 或称为随机变量$X$和$Y$的联合分布函数.

二维随机变量的分布函数的性质:

(1) $F(x,y)$是变量$x$和$y$的不减函数.

(2) $0 \le F(x,y) \le 1$, 且对于任意固定的$y, F(-\infty,y)=0$;对于固定的$x$,有$F(x,-\infty)=0$; 且$F(-\infty, +\infty)=0;F(+\infty,-\infty)=1$.

(3) $F(x,y)=F(x+0,y)=F(x, y+0)$, 即$F(x,y)$关于$x$右连续,关于$y$右连续.

(4) 对于任意的$x_1<x_2, y_1<y_2$, 下述不等式成立

$$F(x_2,y_2)-F(x_2,y_1)-F(x_1,y_2)-F(x_1,y_1) \ge 0$$

$X,Y$的边缘分布函数$F_X(x),F_Y(y)$:

$$F_X(x)=P\{X \le x\} = P\{X \le x, Y < +\infty\}=F(x,+\infty)$$

$$F_Y(y)=P\{Y \le y\} = P\{X < +\infty, Y \le y\}=F(+\infty, y)$$

### 二维离散型随机变量

如果二维随机变量$(X,Y)$的所有可能取的值是有限对或可列多对,则称$(X,Y)$是二维离散想随机变量.

设二维离散型随机变量$(X,Y)$所有可能取的值为$(x_i,y_j)(i,j=1,2,...)$, 其概率记为$P\{X=x_i,Y=y_j\} = p_{ij}(i,j=1,2,...)$,则由概率的定义有

(1) $p_{ij} \ge 0$

(2) $\sum_{i=1}^\infty \sum_{j=1}^\infty p_{ij} = 1$

$(X,Y)$的分布函数为

$$F(x,y)=P\{X \le x, Y\le y\}=\sum_{x_i\le x}\sum_{y_j\le y}P\{X=x_i, Y=y_j\}=\sum_{x_i\le x}\sum_{y_j\le y}p_{ij}$$

$X$的分布律:

$$P\{X=x_i\}=\sum_{j=1}^\infty p_{ij} \triangleq p_{i\cdot} \qquad i=1,2,...$$

$Y$的分布律:

$$P\{Y=y_j\}=\sum_{i=1}^\infty p_{ij} \triangleq p_{\cdot i} \qquad j=1,2,...$$

### 二维连续型随机变量

如果二维随机变量$(X,Y)$的分布函数$F(x,y)$, 存在一个非负可积的二元函数$f(x,y)$,使它对应任意实数$x,y$, 都有

$$F(x,y)=\int_{-\infty}^x \int_{-\infty}^y f(s,t)dsdt$$

则称$(X,Y)$是二维连续型随机变量,函数$f(x,y)$称为二维随机变量$(X,Y)$的概率密度,或称为随机变量$X$和$Y$的联合概率密度.

概率密度$f(x,y)$具有以下性质:

(1) $f(x,y) \ge 0$

(2) $\int_{-\infty}^{+\infty} \int_{-\infty}^{+\infty} f(x,y)dxdy = 1$

(3) 若$f(x,y)$在点$(x,y)$连续, 则有

$$\frac{\partial^2 F(x,y)}{\partial x \partial y}=f(x,y)$$

(4) 随机点$(X,Y)$落在平面区域$D$上的概率为

$$P\{(X,Y) \in D\}=\int \int_D f(x,y) dxdy$$

$X$为连续型变量,其概率密度为

$$f_X(x)=\int_{-\infty}^{+\infty}f(x,y)dy$$

$Y$为连续型变量,其概率密度为

$$f_Y(y)=\int_{-\infty}^{+\infty}f(x,y)dx$$

$X,Y$的联合分布可以确定$X,Y$的边缘分布函数, 反过来,有$X$和$Y$的边缘分布,一般不能确定$X$和$Y$的联合分布.

## 条件分布

### 条件分布律

设$(X,Y)$是离散型随机变量, 可能取值为$(x_i,y_j)(i,j=1,2,...)$, 其分布律及边缘分布律分别为$P\{X=x_i,Y=y_j\}=p_{ij}, P\{X=x_i\}=p_{i\cdot}, P\{Y=y_j\}=p_{\cdot j}$.

若对于固定的$i, P\{X=x_i\} > 0$,则称

$$P\{Y=y_j|X=x_i\}=\frac{P\{X=x_i,Y=y_j\}}{P\{X=x_i\}}=\frac{p_{ij}}{p_{i\cdot}} \triangleq p_{j|i}$$

为在$X=x_i$条件下$Y$的条件分布律.

若对于固定的$j, P\{Y=y_j\}>0$,则称

$$P\{X=x_i|Y=y_j\}=\frac{P\{X=x_i,Y=y_j\}}{P\{Y=y_j\}}=\frac{p_{ij}}{p_{\cdot j}} \triangleq p_{i|j}$$

为在$Y=y_j$条件下$X$的条件分布律.

### 条件分布函数与条件概率密度

由离散型分布函数定义可得条件分布函数为

$$F_{Y|X}(y|x_i)=P\{Y \le y | X=x_i\}=\sum_{y_j\le y} p_{j|i}$$

$$F_{X|Y}(x|y_j)=P\{X \le x | Y=y_j\}=\sum_{x_i\le x} p_{i|j}$$

给定$y$, 设对于任意固定的正数$\varepsilon, P\{y-\varepsilon < Y \le y+\varepsilon \} > 0$, 且若对于任意实数$x$,极限

$$\lim_{\varepsilon \rightarrow 0^+} P\{X \le x | y-\varepsilon < Y \le y+\varepsilon \} = \lim_{\varepsilon \rightarrow 0^+} \frac{P\{X \le x , y-\varepsilon < Y \le y+\varepsilon \}}{P\{y-\varepsilon < Y \le y+\varepsilon \}}$$

存在,则称此极限在条件$Y=y$下$X$的条件分布函数,记为$P\{X \le x | Y=y\}$, 或记为$F_{X|Y}(x|y)$.s

设$(X,Y)$的分布函数为$F(x,y)$,概率密度为$f(x,y)$, 若在点$(x,y)$处$f(x,y)$连续,边缘概率密度$f_Y(y)$连续,且$f_Y(y) > 0$,则有

$$F_{X|Y}(x|y)=\int_{-\infty}^x \frac{f(u,y)}{f_Y(y)} du$$

$$f_{X|Y}(x|y)=\frac{f(x,y)}{f_Y(y)}$$

同理

$$F_{Y|X}(y|x)=\int_{-\infty}^y \frac{f(x,v)}{f_X(x)} dv$$

$$f_{Y|X}(y|x)=\frac{f(x,y)}{f_X(x)}$$

## 相互独立的随机变量

设$F(x,y)$及$F_X(x),F_Y(y)$分别是二维随机变量$(X,Y)$的分布函数及边缘分布函数,若对于所有$x,y$有

$$P\{X\le x, Y\le y\}=P\{X\le x\}P\{Y\le y\}$$

即$F(x,y)=F_X(x)F_Y(y)$, 则称随机变量$X$和$Y$是相互独立的.

### 离散型随机变量

离散型随机变量$X$和$Y$相互独立的充要条件是它们的联合分布函数等于两个边缘分布绿的乘积,即

$$P\{X=x_i,Y=y_j\}=P\{X=x_i\}P\{Y=y_j\}$$
即$p_{ij}=p_{i\cdot} \cdot p_{\cdot j}$ 

### 连续型随机变量

连续型随机变量$X$和$Y$相互独立的充要条件是它们的联合概率密度$f(x,y)$等于边缘概率密度$f_X(x)$和$f_Y(y)$的乘积,即

$$f(x,y)=f_X(x)f_Y(y)$$

## 两个随机变量的函数的分布

### 两个离散型随机变量的函数的分布

$Z=g(X,Y)$的概率分布的一般求法

设$(X,Y)$为离散型随机变量,其概率分布为

$$P\{X=x_i,Y=y_j\} = p_{ij} \qquad i,j=1,2,...$$

则$Z=g(X,Y)$的概率分布的一般求法是:先确定函数$Z=g(X,Y)$的全部可能取值$z=g(x_i,y_j)(i,j=1,2,...)$;再确定相应概率

$$P\{Z=g(x_i,y_j)\}=P\{X=x_i,Y=y_j\}=p_{ij}$$

然后将$z=g(x_i,y_j)(i,j=1,2,...)$中相同的值合并,相应的概率相加,并将$z$值按从小到大的顺序重新排列,且与其概率对应,即可写出$Z=g(X,Y)$的概率分布.

两个离散型随机变量的和的概率公式

$$P\{Z=k\}=\sum_{i=0}^k P\{X=i\}P\{Y=k-i\}=\sum_{j=0}^k P\{Y=j\}P\{X=k-j\}$$

### 两个连续型随机变量的函数的分布

#### 随机变量的和的分布

$$f_Z(z)=\int_{-\infty}^{+\infty}f(z-y,y)dy$$

或

$$f_Z(z)=\int_{-\infty}^{+\infty}f(x,z-x)dx$$

#### 随机变量的商的分布

$$f_Z(z)=\int_{-\infty}^{+\infty}|y|f(yz,y)dy$$

#### 随机变量的极值的分布

设$X,Y$是两个相互独立的随机事件,称$M=max(X,Y)$为最大值变量, $N=min(X,Y)$为最小值变量, 统称为极值变量.

$$F_{max}(z)=P\{M \le z\}=P\{X\le z\}P\{Y\le z\}=F_X(z)F_Y(z)$$

$$\begin{aligned} F_{min}(z) &=P\{N\le z\} \\ &=1-P\{N>z\} \\ &=1-P\{Y>z,X>z\} \\ &=1-P\{X>z\}P\{Y>z\} \\ &=1-[1-F_X(z)][1-F_Y(z)] \end{aligned} $$

## $n(N\ge 2)$维随机变量

### $n(N\ge 2)$维随机变量及其分布

设$E$是一个随机变量,其样本空间为$S=\{e\}$, 设$X_i=X_i(e),(i=1,2,...,n)$是定义在$S$上的$n$个随机变量,由它们构成的一个向量

$$(X_1,X_2,...,X_n)=(X_1(e),X_2(e),...X_n(e)) \qquad e \in S$$

称为$n$维随机向量或$n$维随机变量.

设$(X_1,X_2,...,X_n)$是$n$维随机变量,对于任意实数$x_1,x_2,...,x_n$,$n$元函数

$$F(x_1,x_2,...,x_n)=P\{X_1\le x_1, X_2\le x_2, ..., X_n \le x_n\}$$

称为$n$维随机变量$(X_1,X_2,...,X_n)$的分布函数,或称为随机变量$X_1,X_2,...X_n$的联合分布函数.

若存在非负函数$f(x_1,x_2,...x_n)$, 使对于任意实数$x_1,x_2,...,x_n$,有

$$F(x_1,x_2,...,x_n)=\int_{-\infty}^{x_n}\int_{-\infty}^{x_{n-1}}...\int_{-\infty}^{x_1}f(x_1,x_2,...,x_n)dx_1dx_2...dx_n$$

则称$f(x_1,x_2,...x_n)$为$n$维连续型随机变量$(X_1,X_2,...,X_n)$的概率密度函数.

设$X_i$可能取值为$x_{ij_i}(i=1,2,...,n, \quad j_i=1,2,...)$, 则记

$$P\{X_1=x_{1j_1},X_2=x_{2j_2},...,X_n=x_{nj_n}\}=p_{j_1j_2...j_ns}$$

为$n$为离散型随机变量$(X_1,X_2,...,X_n)$的概率分布或分布律,或随机变量$(X_1,X_2,...,X_n)$的联合分布律.

对于$n$维空间中任一区域$D, \{X_1,X_2,...,X_n\} \in D$ 为一随机事件,若$X_1,X_2,...,X_n$具有概率密度$f(x_1,x_2,...,x_n$, 则概率

$$P\{(X_1,X_2,...,X_n) \in D\}=\int \int ... \int _D f(x_1,x_2,...,x_n)dx_1dx_2...dx_n$$

### $n$个随机变量的相互独立性

若对于所有实数$x_1,x_2,...,x_n$有

$$F(x_1,x_2,...,x_n)=F_{X_1}(x_1)F_{X_2}(x_2)...F_{X_n}(x_n)$$

则称$n$个随机变量$X_1,X_2,...,X_n$是相互独立的.

并且

$$f(x_1,x_2,...,x_n)=f_{X_1}(x_1)f_{X_2}(x_2)...f_{X_n}(x_n)$$

若对所有的实数$x_1,x_2,...,x_m,y_1,y_2,...,y_n$,随机变量$(X_1,X_2,...,X_n,Y_1,Y_2,...,Y_n)$的分布函数$F(x_1,x_2,...,x_m,y_1,y_2,...,y_n)$与关于$(X_1,X_2,...,X_m)$及$(Y_1,Y_2,...,Y_n)$的边缘分布函数$F_1(x_1,x_2,...,x_m), F_2(y_1,y_2,...,y_n)$满足下述等式:

$$F(x_1,x_2,...,x_m,y_1,y_2,...,y_n)=F_1(x_1,x_2,...,x_m)F_2(y_1,y_2,...,y_n)$$

则称随机变量$(X_1,X_2,...,X_m)$与$(Y_1,Y_2,...,Y_n)$是相互独立的.

设$(X_1,X_2,...,X_m)$和$(Y_1,Y_2,...,Y_n)$相互独立,则$X_i(i=1,2,...,m)$与$Y_j(j=1,2,...,n)$相互独立.又若$h,g$是连续函数,则$h(X_1,X_2,...,X_m)$与$g(Y_1,Y_2,...,Y_n)$相互独立.

### $n$维随机变量的函数的分布

设$(X_1,X_2,...,X_n)$为$n$维随机变量,其概率密度为$f(x_1,x_2,...,x_n)$,$g(x_1,x_2,...,x_n)$为$n$元连续函数,则对任意实数$z \in R, Z=g(X_1,X_2,...,X_n)$的分布函数为

$$F_Z(z)=P\{g(X_1,X_2,...,X_n) \le z\}=\int \int ... \int_{D_Z}f(x_1,x_2,...,x_n)dx_1dx_2...dx_n$$

其中$D_Z=\{(x_1,x_2,...,x_n)|g(x_1,x_2,...,x_n) \le z\}$.

# 随机变量的数字特征

## 数学期望

### 数学期望的概念

设离散型随机变量$X$的分布律为

$$P\{X=x_k\}=p_k \qquad k=1,2,...$$

若级数$\sum_{k=1}^{\infty}x_kp_k$绝对收敛,则称级数$\sum_{k=1}^{\infty}x_kp_ks$的值为离散型随机变量$X$的数学期望,记为$E(X)$, 即

$$E(X)=\sum_{k=1}^{\infty}x_kp_k$$

数学期望可简称为期望或均值.

设连续型随机变量$X$的概率密度为$f(x)$,若积分

$$f_{-\infty}^{+\infty}xf(x)dx$$

绝对收敛,则称积分$f_{-\infty}^{+\infty}xf(x)dx$的值为随机变量$X$的数学期望,记为$E(X)$,即

$$E(X)=f_{-\infty}^{+\infty}xf(x)dx$$

### 随机变量的函数的数学期望

设$Y$是随机变量$X$的函数:$Y=g(X)$($g$是连续函数)

1. $X$是离散型随机变量,它的分布律为$p_K=P\{X=x_k\}(k=1,2,...)$,若$\sum_{k=1}^{\infty}g(x_k)p_k$绝对收敛,则有

$$E(Y)=E[g(X)]=\sum_{k=1}^{\infty}g(x_k)p_k$$

2. $X$是连续型随机变量,它的概率密度为$f(x)$,若$\int_{-\infty}^{+\infty}g(x)f(x)dx$绝对收敛,则有

$$E(Y)=E[g(X)]=\int_{-\infty}^{+\infty}g(x)f(x)dx$$

### 数学期望的简单性质

1. (线性法则)设$X$为随机变量,其期望为$E(X)$,对于任意常数$a,b$有

$$E(aX+b)=aE(X)+b$$

2. (加法法则) 设$X,Y$为随机变量,则有

$$E(X+Y)=E(X)+E(Y)$$

3. (乘法法则) 设$X,Y$为两个相互独立的随机变量,则

$$E(XY)=E(X)E(Y)$$

4. (柯西-许瓦兹不等式)

    设$X$与$Y$是两个随机变量,则

$$|E(XY)|^2 \le E(X^2)E(Y^2)$$

## 方差

### 概念

设$X$是一个随机变量,若$E\{[X-E(X)]^2\}$存在,则乘$E\{[X-E(X)]^2\}$称为$X$的方差,记为$D(X)$或$Var(X)$,即

$$D(X)=Var(X)=E\{[X-E(X)]^2\}$$

显然$D(X) \ge 0$, 故在应用中引入与随机变量$X$具有相同量纲的量$\sqrt{D(X)}$, 记为$\sigma(X)$,称为标准差或均方差.

由方差的定义可知,随机变量$X$的方差实际上就是$X$的函数$Y=g(X)=(X-E(X))^2$. 故

若$X$为离散型随机变量,其分布律为$p_k=P\{X=x_k\}(k=1,2,...)$,其方差为

$$D(X)=\sum_{k=1}^{\infty}[x_k-E(X)]^2p_k$$

若$X$为连续型随机变量,其概率密度为$f(x)$,则$X$的方差为

$$D(X)=\int_{-\infty}^{+\infty}[x-E(X)]^2f(x)dx$$

并且具有公式

$$D(X)=E[X^2]-[E(X)]^2$$

### 方差的简单性质

1. 设$X$为随机变量,对于任意的常数$a,b$

$$D(aX+b)=a^2D(X)$$

2. 设$X,Y$为两个相互独立的随机变量,则有

$$D(X+Y)=D(X)+D(Y)$$

3. (契比雪夫不等式) 设$X$为一随机变量,其均值$E(X)=\mu$,方差$D(X)=\sigma^2$,则对任意正数$\sigma > 0$,有

$$P\{|X-\mu|\ge \varepsilon \} \le \frac{\sigma^2}{\varepsilon^2}$$

4. $D(X)=0$的充要条件是$X$以概率1取常数$\mu =E(X)$,即

$$P\{X=\mu \} = 1$$

 ### 几种重要随机变量的数学期望及方差

1. 二项分布$B(n,p)$

    设$X$服从参数为$n,p$的二项分布,其分布律为:

$$P\{X=k\}=\left( \begin{matrix} n \\ k \end{matrix} \right) p^k(1-p)^{n-k}$$

$E(X)=np, \quad D(X)=np(1-p)$

2. 泊松分布$\pi(\lambda)$

    设$X$服从参数为$\lambda$的泊松分布,其 分布律为:

$$P\{X=k\}=\frac{\lambda^ke^{-\lambda}}{k!} \qquad k=0,1,2,...; \lambda>0$$

$E(X)=\lambda \qquad D(X)=\lambda$

3. 几何分布$Ge(p)$

    设$X$服从参数为$p$的几何分布,其分布律为

$$P\{X=k\}=pq^{k-1} \quad k=1,2,.., \quad 0<p<1, q=1-p$$

$E(X)=\frac{1}{p} \qquad D(X)=\frac{q}{p^2}$

4. 均匀分布$U(a,b)$

设在区间$(a,b)$上服从均匀分布, 其概率密度为

$$f(x)=\begin{cases} \frac{1}{b-q} & a<x<b \\ 0 & other \end{cases}$$

$E(X)=\frac{a+b}{2} \qquad D(x)=\frac{(b-a)^2}{12}$

5. 指数分布$Z(\alpha)$

    设$X$服从参数为$\alpha$的指数分布,其概率密度为

$$f(x)=\begin{cases} \alpha e^{-\alpha x} & x>0, \alpha > 0 \\ 0 & x \le 0 \end{cases}$$

$E(X)=\frac{1}{\alpha} \qquad D(X)=\frac{1}{\alpha ^2}$

6. 正态分布$N(\mu, \sigma ^2)$

    设$X$服从参数为$\mu, \sigma ^2$的正态分布,其概率密度为

$$f(X)=\frac{1}{\sqrt{2\pi \sigma}} e ^{-\frac{(x-\mu)^2}{2\sigma ^2}} \qquad \sigma > 0, -\infty < x < +\infty$$

$E(X)=\mu, \qquad D(X)=\sigma ^2$

## 协方差与相关系数

### 概念

设$(X,Y)$为二维随机变量,量$E\{[X-E(X)][Y-E(Y)]\}$称为$X$与$Y$的协方差, 记为$Cov(X,Y)$,即

$$Cov(X,Y)=E\{[X-E(X)][Y-E(Y)]\}$$

而量

$$\rho _{_{XY}}=\frac{Cov(X,Y)}{\sqrt{D(X)}\sqrt{D(Y)}}$$

称为随机变量$X$与$Y$的相关系数, $\rho _{_{XY}}$是一个无量纲的量.

特别的,当$Y=X$时, $Cov(X,X)=D(X)$,此时$\rho _{_{XY}}=1$. 并且

$$D(X+Y)=D(X)+D(Y)+2Cov(X,Y)$$

$$Cov(X,Y)=E(XY)-E(X)E(Y)$$

设$X,Y$为随机变量,$a,b$为任意常数,则协方差$Cov(X,Y)$具有一下性质:

1. $Cov(X,Y)=Cov(Y,X)$

2. $Cov(X+a,Y+b)=Cov(X,Y)$

3. $Cov(aX,bY)=abCov(X,Y)$

4. $Cov(X_1+X_2, Y)=Cov(X_1,Y)+Cov(X_2,Y)$

5. $|Cov(X,Y)| \le \sqrt{D(X)} \sqrt{D(Y)}$

### 相关系数的性质

1. $|\rho _{_{XY}}| \le 1$

2. 若$X,Y$相互独立,且$D(X),D(Y)$存在,则

$$Cov(X,Y)=\rho _{_{XY}}=0$$

如果随机变量$X$与$Y$的相关系数$\rho _{_{XY}}$,则$X$与$Y$不相关.

## 矩及协方差矩阵

### 概念

设$X$和$Y$是随机变量, $k,l$为任一正整数:

(1) 若$E(X^k)$存在,则称$\mu_k=E(X^k)$为$X$的$k$阶原点矩,简称$k$阶距.

(2) 若$E[X-E(X)]^k$存在,则称$\sigma_k=E[X-E(X)]^k$为$X$的$k$阶中心矩.

(3) 若$E(X^kY^l)$存在,则称$\mu_{kl}=E(X^kY^l)$为$X$和$Y$的$k+l$阶混合原点矩.

(4) 若$E\{[X-E(X)]^k[Y-E(Y)]^l\}$存在,则称$\sigma_{kl}=E\{[X-E(X)]^k[Y-E(Y)]^l\}$为$X$和$Y$的$k+l$阶混合中心矩.

显然,$X$的一阶原点矩$E(X)$就是$X$的数学期望,$X$的一阶中心矩$E[X-E(X)]$为$X$的偏差的数学期望,其恒等于0,即

$$E[X-E(X)] = E(X)-E(X)=0$$

而$X$的二阶中心矩$E\{[X-E(X)]^2\}$就是$X$的方差.$X$和$Y$的二阶混合中心矩就是$X$和$Y$的协方差$Cov(X,Y)$.

### 协方差矩阵

设$n$维随机变量$(X_1,X_2,...,X_n)$的二阶混合中心矩

$$C_{ij}=Cov(X_i,Y_j)=E\{[X_i-E(X_i)][Y_j-E(Y_j)]\} \qquad i,j=1,2,...n$$

都存在,则称矩阵

$$C=\left \lgroup \begin{matrix} C_{11} & C_{12} & \cdots & C_{1n} \\ C_{21} & C_{22} & \cdots & C_{2n} \\ \vdots & \vdots & \cdots & \vdots \\ C_{n1} & C_{n2} & \cdots & C_{nn} \end{matrix} \right \rgroup$$

为$n$维随机变量$(X_1,X_2,...,X_n)$的协方差矩阵.由于$C_{ij}=C_{ji}(i,j=1,2,...n)$,因而矩阵$C$为一对称矩阵.

# 大数定律及中心极限定理

## 大数定律$(LLN)$

设$X_1,X_2,...,X_n,...,$是随便变量序列,$E(X_k)(k=1,2,...)$存在. 令$\bar{X}_n=\frac{1}{n}\sum_{k=1}^{n}X_k$,若对于任意给定正数$\varepsilon > 0$, 有

$$\lim_{n \rightarrow \infty}P\{|\bar{X}_n-E(\bar{X}_n)| \ge \varepsilon \} = 0$$

或

$$\lim_{n \rightarrow \infty}P\{|\bar{X}_n-E(\bar{X}_n)| < \varepsilon \} =1 $$

则称$\{X_n\}$服从大数定律或称大数法成立.

(贝努利定理)设$n_A$是$n$次独立重复试验中事件$A$发生的次数,$p$是事件$A$在每次试验中发送的概率,则对于任意的正数$\varepsilon > 0$, 有

$$\lim_{n \rightarrow \infty} P\{|\frac{n_A}{n}-p| < \varepsilon \} = 1 $$

或

$$\lim_{n \rightarrow \infty} P\{|\frac{n_A}{n}-p| \ge \varepsilon \} = 0 $$

契比雪夫特殊情况: 设$X_1,X_2,\cdots,X_n,\cdots$相互独立(即对于任意的$n\ge 1, X_1,X_2,\cdots,X_n$是相互独立的), 且具有相同的数学期望和方差$E(X_k)=\mu, D(X_k)=\sigma ^2(k=1,2,\cdots)$, 则对任意正数$\varepsilon > 0$, 有

$$\lim_{n \rightarrow \infty} P \{|\bar{X}_n - \mu | < \varepsilon \} = 1$$

辛钦定理: 设随机变量序列$X_1,X_2,\cdots,X_n,\cdots$相互独立,服从同一分布,且具有数学期望$E(X_k)=\mu(k=1,2,...)$,则对于任意正数$\varepsilon$有

$$\lim_{n \rightarrow \infty} P\{|\bar{X}_n - \mu| < \varepsilon \} = 1$$

即

$$\bar{X}_n \stackrel{P} \longrightarrow \mu $$

## 中心极限定理$(CLT)$

凡是在一定条件下,断定随机变量序列$X_1,X_2,\cdots$的部分和$Y_n=\sum_{k=1}^{n}X_k$的极限分布为正态分布的定理,均称为中心极限定理.

即中心极限定理应当说明,在何种条件下,下式成立:对任意的$x$,有

$$\lim_{n \rightarrow \infty} P\{\frac{Y_n - E(Y_n)}{\sqrt{D(Y_n)}} \le x \} = \int_{-\infty}^x \frac{1}{\sqrt{2\pi}} e^{-\frac{t^2}{2}}dt=\Phi(x)$$

隶莫佛-拉普拉斯定理

设随机变量列$Y_n(n=1,2,\cdots)$服从参数为$n,p$的二项分布$B(n,p)(0<p<1)$,则对于任意的$x$,恒有

$$\lim_{n \rightarrow \infty} P\{\frac{Y_n - np}{\sqrt{np(1-p)}} \le x \} = \Phi(x)$$

独立同分布中极限定理

设$X_1,X_2,\cdots,X_n,\cdots$相互独立,且服从同一分布,具有数学期望及方差:$E(X_k)=\mu, D(X_k)=\sigma^2 \neq 0(k=1,2,\cdots)$,则随机变量$Y_n=\sum_{k=1}{n}X_k$近似服从正态分布$N(n\mu,n\sigma^2)$,即对于任意的$x$,有

$$\lim_{n\rightarrow \infty}P\{\frac{Y_n - n\mu}{\sqrt{n}\sigma} \le x \} = \Phi(x)$$

李雅普诺夫定理

设随机变量$X_1,X_2,\cdots,X_n$相互独立,它们具有数学期望和方差:

$$E(X_k)=\mu_k, D(X_k)=\sigma_k^2 \neq 0 \qquad k=1,2,\cdots$$

记$B_n^2=\sum_{k=1}^n\sigma_k^2$,若存在正数$\delta$,使得当$n \rightarrow \infty$时,

$$\frac{1}{B_n^{2+\delta}} \sum_{k=1}^nE\{|X_k-\mu_k|^{2+\delta} \} \rightarrow 0$$

则随机变量$Y_n=\sum_{k=1}^nX_k$近似服从正态分布$N(\sum_{k=1}^n\mu_k,B_n^2)$, 即对于任意的$x$,有

$$\lim_{n \rightarrow \infty} P\{\frac{Y_n-\sum_{k=1}^n \mu_k}{B_n} \le x \} = \Phi(x)$$
