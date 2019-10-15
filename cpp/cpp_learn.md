## 4.10 数组的替代品
**数组，vector 和 array**
1. vector 是可变长的动态数组，用的是动态存储，数据存放在堆中，是使用new创建动态数组的替代品，实际上vector类是使用new和delete来管理内存，优点：方便，缺点：效率低
2. array对象类似数组，长度固定，使用静态内存分配，比数组方便和安全。把数组包装成array类，添加安全性。
3. c++不检验越界错误，因此在编写程序中a[-2] = 20.1这种操作是合法的，但是有可能修改了其他地址中的数据，因此非常不安全，在vector和array中也可以进行这种操作，但array和vector用更安全的成员函数at()在避免程序的越界访问。
## 7.2.1 多个参数
如果函数的两个参数的类型相同，则必须分别指定每个参数的类型，不能将声明组合在一齐
```cpp
viod fifi(float a, float b) // valided
viod fofo(float a, b) // not acceptable
```
另外，原型中的变量名不必与定义中的变量名相同，而且可以省略
```cpp
viod n_char(char, int); // valided
```
## 7.3 函数和数组
```cpp
int sum_array(int array[], int n) = int sum_array(int* array, int n)
```