## 4.10 数组的替代品
**数组，vector 和 array**
1. vector 是可变长的动态数组，用的是动态存储，数据存放在堆中，是使用new创建动态数组的替代品，实际上vector类是使用new和delete来管理内存，优点：方便，缺点：效率低
2. array对象类似数组，长度固定，使用静态内存分配，比数组方便和安全。把数组包装成array类，添加安全性。
3. c++不检验越界错误，因此在编写程序中a[-2] = 20.1这种操作是合法的，但是有可能修改了其他地址中的数据，因此非常不安全，在vector和array中也可以进行这种操作，但array和vector用更安全的成员函数at()在避免程序的越界访问。
## 7.2.1 多个参数
如果函数的两个参数的类型相同，则必须分别指定每个参数的类型，不能将声明组合在一齐：
```cpp
viod fifi(float a, float b) // valided
viod fofo(float a, b) // not acceptable
```
另外，原型中的变量名不必与定义中的变量名相同，而且可以省略：
```cpp
viod n_char(char, int); // valided
```
## 7.3 函数和数组
### 7.3.1 函数如何使用指针来处理数组
在cpp仲，当且仅当用于函数头或者函数原型中，int* array和int array[]的含义才是相同的，否则一个表示int变量的指针，另一个表示指向int数组的第一个元素。
**在别的上下文中，也不能用int array[]来声明指针**
```cpp
int sum_array(int array[], int n) = int sum_array(int* array, int n)
// 下面两个等式需要牢记
int arr[5] = {0, 1, 2, 3, 4}
arr[i] == *(arr + i)
&arr[i] == arr + i
arr // 地址
arr[0] // 第一个元素
arr+1 // 第二个元素的地址
```
### 7.3.2 将数组作为参数意味着什么
在函数调用中，传递常规变量时，函数将使用该变量的拷贝，但传递数组时，函数将使用原来的数组。这种区别不违反cpp按值传递的方法，因为函数仍然传递了一个值，这个值被赋给一个新的变量，不同的是这个值是一个地址，而不是数组的内容。
```cpp
/*
* 为将数组类型和元素数量告诉数组来处理函数，通过不同的参数来传递
*/
viod fillArray(int arr[], int size);	// prototype
/*
* 不要试图使用方括号表示法来传递数组长度
*/
viod fillArray(int arr[size]); // bad prototype
```

### 7.3.5 指针与const
1. 让指针指向一个常量对象，防止使用该指针来修改所指向的值
2. 将指针本身设为常量，这样可以防止改变指针指向指向的位置
```cpp
int age = 39;
const int* pt = &age; // 指向常量的指针pt，pt指向一个const int
*pt += 1;	// invalid
cin >> *pt;	// invalid
*pt = 20;	// invalid
age = 20;	// valid
/*
* 这里声明指出pt指向一个const int 说明pt认为他指向的值是常量，
* 因此不能通过来修改age的值，但是他认为age是常量，实际上这个变量
* 不一定是常量，依然可以通过变量来修改pt指向的值
*/
```