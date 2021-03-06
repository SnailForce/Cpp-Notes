# C++ 内存四区

## 栈 stack

编译器自动分配与释放

- 存放为运行时函数分配的局部变量、函数参数、返回数据、返回地址
- 操作类似于数据结构中的栈
- 效率高，分配内存容量有限

## 堆 heap

程序员自动分配，如果程序员没有释放，程序结束后可能有OS回收

- 分配类似于链表
- 使用灵活，生命周期由程序员决定，易出现内存泄漏，频繁分配和释放会产生内存碎片

## 全局区 静态区 static

程序结束后由OS释放

- 存放为全局变量、静态数据、常量
- 全局区分为已初始化全局区（data）和未初始化全局区（bss）
- 在 C 语言中，全局变量又分为初始化的和未初始化的（未被初始化的对象存储区可以通过 void* 来访问和操纵，程序结束后由系统自行释放），在 C++ 里面没有这个区分了，他们共同占用同一块内存区。

## 常量区

程序结束后OS释放

- 存放常量字符串

## 代码区

- 存放函数体（类成员函数和全局区）的二进制代码

## 内存分配简易图

![img](.assets/20180813110942795)

![img](.assets/20161029171857434)

## stack 和 heap 的区别

1. 管理方式不同：栈是由编译器自动申请和释放空间，堆是需要程序员手动申请和释放；

2. 空间大小不同：栈的空间是有限的，在32位平台下，VC6下默认为1M，堆最大可以到4G；
   能否产生碎片：栈和数据结构中的栈原理相同，在弹出一个元素之前，上一个已经弹出了，不会产生碎片，如果不停地调用malloc、free对造成内存碎片很多；

3. 生长方向不同：堆生长方向是向上的，也就是向着内存地址增加的方向，栈刚好相反，向着内存减小的方向生长。

4. 分配方式不同：堆都是动态分配的，没有静态分配的堆。栈有静态分配和动态分配。静态分配是编译器完成的，比如局部变量的分配。动态分配由 malloc 函数进行分配，但是栈的动态分配和堆是不同的，它的动态分配是由编译器进行释放，无需我们手工实现。

5. 分配效率不同：栈的效率比堆高很多。栈是机器系统提供的数据结构，计算机在底层提供栈的支持，分配专门的寄存器来存放栈的地址，压栈出栈都有相应的指令，因此比较快。堆是由库函数提供的，机制很复杂，库函数会按照一定的算法进行搜索内存，因此比较慢。

   原文链接：https://blog.csdn.net/cherrydreamsover/article/details/81627855

静态全局变量的作用域局限于一个源文件内，只能为该源文件内的函数公用