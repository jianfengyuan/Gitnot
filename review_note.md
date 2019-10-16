## 机器学习
### 1. 机器学习分类
监督学习：有标记
&emsp;&emsp;判别模型：对于数据模型化，直接根据模型生成结果
&emsp;&emsp;生成模型：根据已知属性生成概率
非监督学习：无标记

### 2. 线性回归 linear regression
#### 2.1 目标
&emsp;&emsp;找出一组w尽可能好地描述数据，即预测值与真实值尽可能小，最小化损失函数，常用作数值回归任务
#### 2.2 损失函数
$$ l=\sum_{i=0}^n \hat{y}^i-y^i $$
#### 2.3 求解
1. 闭合公式求解
分别对w和b求偏导，令两个偏导公式为0，分别求出w和b的值
2. 梯度下降

### 3.逻辑回归 logistics regression
#### 3.1 目标
&emsp;&emsp;通过y对x 的概率分别进行建模，结果为该判断为该标记的概率，常用作类型判别任务
#### 3.2 损失函数 
$$ 
L(\mathbf{w}) = \prod_{i=1}^n p(\mathbf{x}^{(i)})^{y(i)} (1-p(\mathbf{x^{(i)}}))^{1-y^{(i)}}
$$
连成会造成数值下溢，因此对$p(\mathbf{x})$使用对数概率
$$
l(\mathbf{w}) = \sum_{i=1}^n log(p(\mathbf{x}^{(i)})){y(i)} + log(1-p(\mathbf{x^{(i)}})({1-y^{(i)}})
$$
#### 3.3 求解
&emsp;&emsp;没有闭式求解，只能使用<font color="red">梯度上升</font>，==最大化似然估计==

### 4. 支持向量机 SVM
#### 4.1 基础术语
##### 4.1.1 划分超平面
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
##### 4.1.3 间隔 margin
&emsp;&emsp;上面两条直线的距离为$D=d_1+d_2=\frac{2}{\Vert\mathbf{W}\Vert}$这被称为间隔（margin）$\gamma$
##### 4.1.4 SVM 目标
最大化margin，找出一个超平面，令不同数据尽可能清楚地分隔开
$$
max\ {\gamma} = max\frac{2}{\|w\|} \ = \ min\frac{1}{2}\Vert\mathbf{W}\Vert \ \longrightarrow \ min\frac{1}{2}\Vert\mathbf{W}\Vert^{2}\ = \ min\frac{1}{2}\mathbf{W}^T\mathbf{W}
$$
##### 4.1.4 SVM分类
硬间隔SVM，软间隔SVM，核函数SVM

### 最优化问题
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
\frac{\partial{F(x)}}{\partial{x_i}} =0 \quad ... \quad \frac{\partial{F(x)}}{\partial{\lambda_{k}}} =0
$$
如果有l个约束条件，就应该有l+1个方程，方程组的解就是可能的最优化值
最优化问题会碰到一下三种情况
- 无约束条件
这是最简单的情况，解决方法通常是函数对变量求导，令求导函数等于0的点可能是极值点。将结果带回原函数进行验证即可。
- 等式约束条件
设目标函数为$f(x)$，约束条件为$h_k(x)$
- 不等式约束条件
设目标函数为$f(x)$,同时含有等式约束条件$h_k(x)$和不等式条件$g_k(x)$
$$
\begin{array}{ll}
min\ f(x)\\
st.\ h_k(x) = 0 \ k =1,2,3 ...,l \\ g_k(x) \le 0 \ k = 1,2,3 ....l
\end{array}
$$