# allocator

allocator类定义在头文件memory中，用于将内存分配和对象构造分离开，分配的内存是原始未构造的

为什么会有allocator?

 原因是new在内存分配上面有一些局限性，new的机制是将内存分配和对象构造组合在一起，同样的，delete也是将对象析构和内存释放组合在一起。但当分配一块大块内存时，我们想要自己在这块内存上构建对象，就像建房子，我们弄到一块地，想自己开发更赚钱，或更满足自己的需求，这中情况下我们希望将内存分配和对象构造分离，这样就可实现，我们可以事先得到大块内存，然后真正需要时就在这块内存上创建对象。

[C++中的allocator类（内存分配器）](https://blog.csdn.net/u012333003/article/details/22104939)

[样例](https://www.geeksforgeeks.org/stdallocator-in-cpp-with-examples/)