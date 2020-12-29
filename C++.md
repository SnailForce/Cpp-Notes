

# C++

## 基础

函数签名包含形参类别和函数名字，返回值类别和形参名字不属于签名的组成部分，const是函数签名的一部分

将`float`转换为`int`和`double`，C++更喜欢转换为`double`

 **const_iterator**等价于指向常量的指针

移动操作仅当类没有显式声明移动操作，拷贝操作，析构时才自动生成

用户声明移动操作，拷贝构造和拷贝赋值运算符是delete

用户声明析构函数，拷贝操作不再自动生成

确定了指针所指，知道销毁机制，也很难确定你在所有执行路径上都执行了销毁操作（包括异常产生后的路径）。少一条路径就会产生资源泄漏，销毁多次还会导致未定义行为

要正确的模拟原生制作需要移动语义，但是C++98没有这个东西。取而代之，`std::auto_ptr`拉拢拷贝操作来达到自己的移动意图。这导致了令人奇怪的代码（拷贝一个`std::auto_ptr`会将它本身设置为null！）和令人沮丧的使用限制（比如不能将`std::auto_ptr`放入容器）

原子操作通常比非原子操作要慢

对于`std::unique_ptr`来说，销毁器类型是智能指针类型的一部分。对于`std::shared_ptr`则不是

`std::unique_ptr`把销毁器视作类型的一部分

C++ 不允许直接将void * 隐式转换到其他类型

nullptr 的类型为nullptr_t，能够隐式的转换为任何指针或成员指针的类型，也能和他们进行相等或者不等的比较

模板是用来产生类型的

被捕获的变量在 lambda 表达式被创建时拷贝，而非调用时才拷贝

函数 指针的调用不是类型安全的

纯右值 (prvalue, pure rvalue)，纯粹的右值，要么是纯粹的字面量，例如 10, true；要么是求值 结果相当于字面量或匿名临时对象，例如 1+2。非引用返回的临时变量、运算表达式产生的临时变量、原 始字面量、Lambda 表达式都属于纯右值

字符串字面量只有在类中才是右值，当其位于普通函数中是左值

非常量左引用无法引用右值

std::array 不会自动退化成 T*

 C++ 保证了所有栈对象在声明周期结束时会被销毁

move和forward在运行期不会生成可执行代码

函数形参皆为左值

![preview](C++.assets\v2-496422d37709e10155089f5f978f2782_r.jpg)

类型是右值引用 但是是左值 

1. 以下语法形式将把表达式 t 转换为T类型的右值（准确的说是无名右值引用，是右值的一种）
   static_cast<T&&>(t)
2. 无名的右值引用是右值
   具名的右值引用是左值
3. 函数模板参数推导规则（右值引用参数部分）：
   当函数模板的模板参数为T而函数形参为T&&（右值引用）时适用本规则。
   若实参为左值 U& ，则模板参数 T 应推导为引用类型 U& 。
   （根据引用折叠规则， U& + && => U&， 而T&& ≡ U&，故T ≡ U& ）
   若实参为右值 U&& ，则模板参数 T 应推导为非引用类型 U 。
   （根据引用折叠规则， U或U&& + && => U&&， 而T&& ≡ U&&，故T ≡ U或U&&，这里强制规定T ≡ U ）

RVO返回值优化

前提条件

1. 局部对象型别和函数返回值型别相同
2. 返回的是局部对象本身

完美转发会避免创建临时对象

在C++中，**static静态成员变量不能在类的内部初始化**。在类的内部只是声明，定义必须在类定义体的外部，通常在类的实现文件中初始化，如：double Account::Rate = 2.25;static关键字只能用于类定义体内部的声明中，定义时不能标示为static

闭包是lambda式创建的运行期对象

lambda捕获表达式所在作用域内可见的非静态局部变量（包括形参）

通过字符串创建 std::regex 要求相对较⻓的运⾏时开

new：先分配memory, 再調用ctor

delete：先調用dtor, 再釋放memory

Composition 复合关系 has-a queue has a deque

![image-20201204160630490](C++.assets\image-20201204160630490.png)

Delegation 委托关系 pImpl

![image-20201204160702036](C++.assets\image-20201204160702036.png)

Inheritance 继承关系 is-a

![image-20201204160745675](C++.assets\image-20201204160745675.png)

![image-20201204160755250](C++.assets\image-20201204160755250.png)

![image-20201207155043864](C++.assets\image-20201207155043864.png)

只要类中有虚函数，对象中会多一个虚函数指针（vptr）（内存+4）

子类继承函数，继承的是父类函数的调用权不是内存大小

![image-20201207160135976](C++.assets\image-20201207160135976.png)

静态绑定 CALL xxx 汇编语言

动态绑定 指针调用 向上转型（父类指向子类） 调用虚函数

![image-20201207164159541](C++.assets\image-20201207164159541.png)

重载了函数调用操作符（即，operator()）的任何类叫做仿函数类。从这样的类建立的对象称为函数对象或仿函
数

new expression表达式是不能重载的，new调用的函数是可以重载的

1. 各类继承
2. 智能指针
3. 转换

![image-20201208112405322](C++.assets\image-20201208112405322.png)

拷贝构造函数和拷贝赋值函数无法重载

模板声明只允许在全局、命名空间或类范围内

override 要求函数签名完全相同

移动构造函数和移动赋值函数要求noexcept

析构函数默认是noexcept

定义一个函数为虚函数，不代表函数为不被实现的函数。

定义它为虚函数是为了允许用基类的指针来调用子类的这个函数。

定义一个函数为纯虚函数，才代表函数没有被实现。

定义纯虚函数是为了实现一个接口，起到一个规范的作用，规范继承这个类的程序员必须实现这个函数。

当使用类的指针调用成员函数时，普通函数由指针类型决定，而虚函数由指针指向的实际类型决定

[纯虚函数](https://zhuanlan.zhihu.com/p/37331092)

## STL

### STL 容器

| 容器                                                         | 底层数据结构      | 时间复杂度                                                   | 有无序 | 可不可重复 | 其他                                                         |
| ------------------------------------------------------------ | ----------------- | ------------------------------------------------------------ | ------ | ---------- | ------------------------------------------------------------ |
| [array](https://github.com/huihut/interview/tree/master/STL#array) | 数组              | 随机读改 O(1)                                                | 无序   | 可重复     | 支持随机访问                                                 |
| [vector](https://github.com/huihut/interview/tree/master/STL#vector) | 数组              | 随机读改、尾部插入、尾部删除 O(1)<br/>头部插入、头部删除 O(n) | 无序   | 可重复     | 支持随机访问                                                 |
| [deque](https://github.com/huihut/interview/tree/master/STL#deque) | 双端队列          | 头尾插入、头尾删除 O(1)                                      | 无序   | 可重复     | 一个中央控制器 + 多个缓冲区，支持首尾快速增删，支持随机访问  |
| [forward_list](https://github.com/huihut/interview/tree/master/STL#forward_list) | 单向链表          | 插入、删除 O(1)                                              | 无序   | 可重复     | 不支持随机访问                                               |
| [list](https://github.com/huihut/interview/tree/master/STL#list) | 双向链表          | 插入、删除 O(1)                                              | 无序   | 可重复     | 不支持随机访问                                               |
| [stack](https://github.com/huihut/interview/tree/master/STL#stack) | deque / list      | 顶部插入、顶部删除 O(1)                                      | 无序   | 可重复     | deque 或 list 封闭头端开口，不用 vector 的原因应该是容量大小有限制，扩容耗时 |
| [queue](https://github.com/huihut/interview/tree/master/STL#queue) | deque / list      | 尾部插入、头部删除 O(1)                                      | 无序   | 可重复     | deque 或 list 封闭头端开口，不用 vector 的原因应该是容量大小有限制，扩容耗时 |
| [priority_queue](https://github.com/huihut/interview/tree/master/STL#priority_queue) | vector + max-heap | 插入、删除 O(log<sub>2</sub>n)                               | 有序   | 可重复     | vector容器+heap处理规则                                      |
| [set](https://github.com/huihut/interview/tree/master/STL#set) | 红黑树            | 插入、删除、查找 O(log<sub>2</sub>n)                         | 有序   | 不可重复   |                                                              |
| [multiset](https://github.com/huihut/interview/tree/master/STL#multiset) | 红黑树            | 插入、删除、查找 O(log<sub>2</sub>n)                         | 有序   | 可重复     |                                                              |
| [map](https://github.com/huihut/interview/tree/master/STL#map) | 红黑树            | 插入、删除、查找 O(log<sub>2</sub>n)                         | 有序   | 不可重复   |                                                              |
| [multimap](https://github.com/huihut/interview/tree/master/STL#multimap) | 红黑树            | 插入、删除、查找 O(log<sub>2</sub>n)                         | 有序   | 可重复     |                                                              |
| [unordered_set](https://github.com/huihut/interview/tree/master/STL#unordered_set) | 哈希表            | 插入、删除、查找 O(1) 最差 O(n)                              | 无序   | 不可重复   |                                                              |
| [unordered_multiset](https://github.com/huihut/interview/tree/master/STL#unordered_multiset) | 哈希表            | 插入、删除、查找 O(1) 最差 O(n)                              | 无序   | 可重复     |                                                              |
| [unordered_map](https://github.com/huihut/interview/tree/master/STL#unordered_map) | 哈希表            | 插入、删除、查找 O(1) 最差 O(n)                              | 无序   | 不可重复   |                                                              |
| [unordered_multimap](https://github.com/huihut/interview/tree/master/STL#unordered_multimap) | 哈希表            | 插入、删除、查找 O(1) 最差 O(n)                              | 无序   | 可重复     |                                                              |

## 算法

### 排序

### 查找

## 设计模式GOF

![image-20201217171223102](C++.assets\image-20201217171223102.png)




### 创建型

- [x] 单例模式
- [x] 工厂方法模式
- [x] 抽象工厂模式
- [x] 策略模式

### 结构型

- [ ] 代理模式

- [x] 装饰者模式

- [x] 适配器模式


### 行为型

- [x] 观察者模式


## 数据库

## 操作系统

## 网络

