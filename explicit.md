# explicit

限制隐式转换

explicit关键字只对有一个参数的类构造函数有效, 如果类构造函数参数大于或等于两个时, 是不会产生隐式转换的, 所以explicit关键字也就无效了。

有一个例外, 就是当除了第一个参数以外的其他参数都有默认值的时候, explicit关键字依然有效, 此时, 当调用构造函数时只传入一个参数, 等效于只有一个参数的类构造函数。

explicit只能写在在声明中，不能写在定义中

copy constructor不要声明为explicit

[](https://www.cnblogs.com/dwdxdy/archive/2012/07/17/2595479.html)