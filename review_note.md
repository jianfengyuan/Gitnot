# 机器学习
## 1. 机器学习分类
监督学习：有标记
&emsp;&emsp;判别模型：对于数据模型化，直接根据模型生成结果
&emsp;&emsp;生成模型：根据已知属性生成概率
非监督学习：无标记

## 2. 线性回归 linear regression
### 2.1 目标
&emsp;&emsp;找出一组w尽可能好地描述数据，即预测值与真实值尽可能小，最小化损失函数，常用作数值回归任务
#### 2.2 损失函数
$$ l=\sum_{i=0}^n \hat{y}^i-y^i $$
### 2.3 求解
1. 闭合公式求解
分别对w和b求偏导，令两个偏导公式为0，分别求出w和b的值
2. 梯度下降

## 3.逻辑回归 logistics regression
### 3.1 目标
&emsp;&emsp;通过y对x 的概率分别进行建模，结果为该判断为该标记的概率，常用在分类任务
### 3.2 损失函数 
$$ 
L(\mathbf{w}) = \prod_{i=1}^n p(\mathbf{x}^{(i)})^{y(i)} (1-p(\mathbf{x^{(i)}}))^{1-y^{(i)}}
$$
连成会造成数值下溢，因此对$p(\mathbf{x})$使用对数概率
$$
l(\mathbf{w}) = \sum_{i=1}^n log(p(\mathbf{x}^{(i)})){y(i)} + log(1-p(\mathbf{x^{(i)}}))({1-y^{(i)}})
$$
#### 3.3 求解
&emsp;&emsp;没有闭式求解，只能使用<font color="red">梯度上升</font>，==最大化似然估计==

## 4. 支持向量机 SVM
### 4.1 基础术语
#### 4.1.1 划分超平面
划分超平面是根据两个类的最靠近划分超平面的样本决定的，这两个样本到划分超平面的的距离分别为$d1$和$d2$
##### 4.1.2 平面之间的距离和平行线之间的距离
两平面之间的距离可以看做两条直线的距离  
假设两个分界线的方程为
$$
\begin{cases}
\mathbf{W}^{T}\mathbf{X} + b = 1 \\
\mathbf{W}^{T}\mathbf{X} + b =-1
\end{cases}
$$
则这两条直线到超平面的距离可以写成$d_1 = \frac{\lvert1\rvert}{\Vert\mathbf{W}\Vert}$  $d_2=\frac{\vert-1\vert}{\Vert\mathbf{W}\Vert}$
#### 4.1.3 间隔 margin
&emsp;&emsp;上面两条直线的距离为$D=d_1+d_2=\frac{2}{\Vert\mathbf{W}\Vert}$这被称为间隔（margin）$\gamma$
#### 4.1.4 SVM 目标
最大化margin，找出一个超平面，令不同数据尽可能清楚地分隔开
$$
max\ {\gamma} = max\frac{2}{\|w\|} \ = \ min\frac{1}{2}\Vert\mathbf{W}\Vert \ \longrightarrow \ min\frac{1}{2}\Vert\mathbf{W}\Vert^{2}\ = \ min\frac{1}{2}\mathbf{W}^T\mathbf{W}
$$
#### 4.1.5 SVM分类
硬间隔SVM，软间隔SVM，核函数SVM
### 4.2 硬间隔支持向量机求解
假设两种不同点的方程有
$$
\begin{cases}
\mathbf{W}^{T}\mathbf{X} + b \ge 1 \\
\mathbf{W}^{T}\mathbf{X} + b \le -1
\end{cases}
$$
则对每个样本点都可以写作$y_i(\mathbf{w}^T\mathbf{x}+b) \ge 1$ 写作KKT条件形式为$1-y_i(\mathbf{w}^T\mathbf{x}+b) \le 0$
因为$min\frac{1}{2}\mathbf{W}^T\mathbf{W}$是凸函数，因此可以引入拉格朗日乘子法和KKT条件进行二次规划求解
写成拉格朗日函数的形式，分别对$\mathbf{w}$和$b$求偏导得出$w=\sum_{i=0}^N\alpha_iy_ix_i$和$\sum_{i=0}^{N}\alpha_iy_i=0$
将其代入拉格朗日函数$L(\mathbf{w},b,\alpha)$得到$\mathbf{w}$关于$\alpha$的函数
此时，原问题变为其对偶问题，即从$min\frac{1}{2}\Vert\mathbf{W}\Vert^{2}$变成求$max\ \mathbf{w}(\alpha) \ st.\ \alpha_i \ge0 \quad \sum_{i=0}^{N}\alpha_iy_i=0$

以上情况只针对数据完全线性可分的情况，称为硬间隔支持向量机
### 4.3 软间隔支持向量机
若数据包含噪声或者不可完全线性分割，则对每个样本引入<font color="red">松弛变量&ensp;$\xi
\ge 0$</font>，称为软间隔支持向量机
两个分界线方程重写为
$$
\begin{cases}
\mathbf{W}^{T}\mathbf{X} + b = 1-\xi,\ y_i=1 \\
\mathbf{W}^{T}\mathbf{X} + b =-1 + \xi,\ y_i = -1
\end{cases}
$$
### 4.4决策树的优缺点
- 优点：
高准确率，分类速度快，能解决特征数量大于样本数量的情况，因为有核函数，因此可以适应不同的对象
- 缺点：
需要调整超参数，当样本数量大的时候，训练速度慢

## 5.决策树
### 5.1 熵
#### 5.1.1 信息熵
衡量数据集的不确定性，即信息量的大小
$$
Ent(D) = -\sum_{k=1}^{\vert y \vert}p_{k}log_{2}p_k
$$
#### 5.1.2 交叉熵
用来衡量在给定的真实分布下，使用非真实分布指定的策略消除系统的不确定性所需要付出努力的大小
$$
H(P,Q) = \sum_iP(i)log_a\frac{1}{Q(i)}
$$
#### 5.1.3 相对熵
用来衡量两个概率分布之间的差异，也叫KL散度
$$
D_{KL}(P||Q) = \sum_{i}P(i)log_a\frac{P(i)}{Q(i)}
$$
### 5.2 ID3
#### 5.2.1 启发式
信息增益
$$
Gain(S,A) = Ent(S) - \sum_{v\in V(A)}\frac{\vert S_v\vert}{\vert S \vert}Ent(S_{v})
$$
$v$是属性$A$的某个值，S是父节点子集，$S_v$是父节点子集下$A$属性为$v$的子集
#### 5.2.2 特点
分裂节点越多越细，信息增益越大，因此趋向使用多值属性生长决策树，ID3只能处理离散数据，不能处理连续数值数据
### 5.3 C4.5
#### 5.3.1 启发式
信息增益率
$$
\begin{aligned}
Gainratio(S,A) = \frac{Gain(S,A)}{IV(A)} \\
IV(A) = -\sum\frac{\vert S_V\vert}{\vert S\vert}log\frac{\vert S_V\vert}{\vert S\vert}
\end{aligned}
$$
#### 5.3.2 特点
$IV(A)$会随着$A$的取值个数增多而增多，因此使用信息增益率来划分的决策树会趋向使用属性值少的属性进行分裂
#### 5.3.3 实际问题
在现实中有可能出现$\vert S_v\vert = \vert S\vert$的现象，此时GainRatio的分子$IV(A)$会趋于0,增益率会变得非常大
因此C4.5会先使用信息增益大于阈值的属性，再使用信息增益率选出最优分割属性。
#### 5.3.4 如何处理连续数值数据
### 5.4 CART
#### 5.4.1 启发式
基尼系数
$$

$$
#### 5.4.2 特点
### 5.5 GBDT


## 激励函数 Activation Function

## 正则化 （Regularization）
### L1正则化
### L2正则化


## 最优化问题
常用工具: <font color="blue"> **拉格朗日乘子法**，**KKT条件**</font>
**拉格朗日乘子法**
设目标函数为$f(x)$，约束条件为$h_k(x)$
$$
\begin{array}{ll}
min\ f(x)\\
st.\ h_k(x) = 0 \ k =1,2,3 ...,l
\end{array}
$$
则定义拉格朗日函数为$F(x)$
$$F(x,\lambda) = f(x) + \sum_{k=1}^{l}\lambda_{k}h_{k}(x)$$
其中$\lambda_k$是各个约束条件的待定系数
然后解各个变量的偏导数
$$
\frac{\partial{F(x)}} {\partial{x_i}} = 0 \quad ... \quad \frac{\partial{F(x)}} {\partial{\lambda_{k}}} =0
$$
如果有$l$个约束条件，就应该有$l+1$个方程，方程组的解就是可能的最优化值
最优化问题会碰到一下三种情况
- 无约束条件
这是最简单的情况，解决方法通常是函数对变量求导，令求导函数等于0的点可能是极值点。将结果带回原函数进行验证即可。
- 等式约束条件
设目标函数为$f(x)$，约束条件为$h_k(x)$
则定义拉格朗日函数为$F(x)$
$$F(x,\lambda) = f(x) + \sum_{k=1}^{l}\lambda_{k}h_{k}(x)$$
- 不等式约束条件
设目标函数为$f(x)$,同时含有等式约束条件$h_k(x)$和不等式条件$g_k(x)$
$$
\begin{array}{c}
min\ f(x)\\
st.\ h_k(x) = 0 \ k =1,2,3 ...,l \\ g_k(x)  \le 0 \ k = 1,2,3 ....l \quad\color{red}{(must\ in\ \le\ form)}
\end{array}
$$
则拉格朗日函数$F(X)$可以写成
$$F(x,\lambda) = f(x) + \sum_{j=1}^{p}\lambda_{j}h_{j}(x)+\sum_{k=1}^{q}\mu_{k}h_{k}(x)$$
要解上述问题，必须满足KKT条件

**KKT条件**
$$
\begin{array}{c}
\frac{\partial L}{\partial X} \vert_{X=X^*} = 0  \quad (1)\\ 
\lambda_j \ne 0 \quad (2)\\
\mu_k \ge 0 \quad (3)\\
\mu_{k}g_{k}(X^{*}) = 0  \quad (4)\\
h_j(X^{*}) = 0 \quad j = 1,2,3...l \quad (5)\\
g_k(x)  \le 0 \ k = 1,2,3 ...l \quad (6)
\end{array}
$$
(1)是对拉格朗日函数取极值时候带来的一个必要条件，(2)是拉格朗日系数约束（同等式情况），(3)是不等式约束情况，(4)是互补松弛条件，(5)、(6)是原约束条件。
