# NULL and nullptr

## C

```c
#define NULL ((void*)0)
```

## C++

```c++
#define NULL 0
```

C++中不能将void *类型的指针**隐式转换**成其他指针类型

nullptr并非整型类别，甚至也不是指针类型，但是能转换成任意指针类型。nullptr的实际类型是std:nullptr_t

如果只有f(int *)，则f(NULL)会调用该函数；如果有f(int)和f(int *)，则f(NULL)会调用f(int)，存在二义性