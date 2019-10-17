# 深度学习
## 1. Back propagation
![title](https://i.loli.net/2019/10/17/cMwIxP3Hh71lTCv.png)
目标：$\frac{\partial L(\theta)}{\partial w}$
因为$\frac{\partial L(\theta)}{\partial w}=\sum_{n=1}^{N}\frac{\partial C^n(\theta)}{\partial w}$, 因此目标可以看做$\frac{\partial C}{\partial w}$
这里$\sum_{n=1}^{N}C^n(\theta)$就是指loss function
根据链式法则
$\frac{\partial C}{\partial w}=\frac{\partial z}{\partial w}\frac{\partial C}{\partial z}$
这里$\frac{\partial z}{\partial w}$称为forward pass项，偏导结果就是输入值
$\frac{\partial C}{\partial z}$称为backward pass项，从最后一层结果望前推倒
以图片中的neural network为例子，设$C$为loss function的结果，刺激函数为sigmoid $\sigma(z)$,则sigmoid function的导数$\sigma'(z)$也已知，且为常数，设$y_1$就是activation function的结果
根据链式法则
$$
\frac{\partial C}{\partial z_5}=\frac{\partial C}{\partial y_1}\frac{\partial y_1}{\partial z_5}=\sigma'(z_5)\frac{\partial C}{\partial y_1}
$$
其中$C=\frac{1}{2}(\hat y_1-y_1)^2 + \frac{1}{2}(\hat y_2-y_2)^2$，同理可求$\frac{\partial C}{\partial z_6}$
若要求$\frac{\partial C}{\partial z_3}$，则可以看做一个反向的neural network
$$
\frac{\partial C}{\partial z_3}=(\frac{\partial C}{\partial z_5}*w +\frac{\partial C}{\partial z_6}*w')\sigma'(z_3)
$$
## 2. CNN
## 3. RNN
## 4. LSTM
## 5. BN
![title](https://i.loli.net/2019/10/17/EIviD56BCK4Z9qM.png)
![title](https://i.loli.net/2019/10/17/MVrPFvS3I495cnB.png)
![title](https://i.loli.net/2019/10/17/OBzxGF7tkCoL5Ay.png)