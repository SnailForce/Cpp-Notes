# const

const 左结合

顶层const表示const定义的变量本身是个常量， 底层const表示定义变量所指对象是一个常量

在类中将成员函数修饰为const，const修饰this指针指向的对象，这也就保证调用这个const成员函数的对象在内部不会被改变

表明在该函数体内，不能修改对象的数据成员而且不能调用非const函数

为什么不能调用非const函数？因为非const函数可能修改数据成员，const成员函数是不能修改数据成员的, 所以在const成员函数内只能调用const函数

众所周知，在相同参数及相同名字的情况下，const是可以构成函数重载的，但const成员函数不能更改任何非静态成员变量

作为一种良好的编程风格，在声明一个成员函数时，若该成员函数并不对数据成员进行修改操作，应尽可能将该成员函数声明为const 成员函数。

 类中二函数都存在的情况下：

const对象默认调用const成员函数，非const对象默认调用非const成员函数；

若非const对象想调用const成员函数，则需显式转化，如(const Student&)obj.getAge();

若const对象想调用非const成员函数，同理const_cast<Student&>(constObj).getAge();(注意：constObj要加括号)

类中只有一函数存在的情况下：

非const对象可以调用const成员函数或非const成员函数；

const对象只能调用const成员函数,直接调用非const函数时编译器会报错；

const成员函数可以访问非const对象的非const数据成员、const数据成员，也可以访问const对象内的所有数据成员；

非const成员函数可以访问非const对象的非const数据成员、const数据成员，但不可以访问const对象的任意数据成员；



