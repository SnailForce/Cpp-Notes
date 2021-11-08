# assert

assert   断言，运行时判断，无要求，比较方便
static_assert  静态断言，编译时判断，需要判断的表达式是常量，即在编译时即可运算的，所以判断的范围比较局限

assert不是函数 是宏，从而保证debug版本和release版本没有区别