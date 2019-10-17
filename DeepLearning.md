# 深度学习
## 1. Back propagation
![title](https://i.loli.net/2019/10/17/cMwIxP3Hh71lTCv.png)
目标：$\frac{\partial L(\theta)}{\partial w}$
因为$\frac{\partial L(\theta)}{\partial w}=\sum_{n=1}^{N}\frac{\partial C^n(\theta)}{\partial w}$, 因此目标可以看做$\frac{\partial C}{\partial w}$
这里$\sum_{n=1}^{N}C^n(\theta)$就是指loss function
根据链式法则
$\frac{\partial C}{\partial w}=\frac{\partial z}{\partial w}\frac{\partial C}{\partial z}$
这里$\frac{\partial z}{\partial w}$称为forward pass项，偏导结果就是输入值
$\frac{\partial C}{\partial z}$称为backward pass项
## 2. CNN
## 3. RNN
## 4. LSTM
## 5. BN