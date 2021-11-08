# alloc

alloca是向栈申请内存,因此无需释放

malloc 申请空间但不初始化 void *malloc(unsigned int num_bytes)；

calloc 申请空间初始化为0 效率低 void *calloc(size_t n, size_t size)；

 realloc 空间扩容 void realloc(void *ptr, size_t new_Size)；

realloc(p, 0);  // 相当于free(p)

[malloc、calloc、realloc的区别](https://blog.csdn.net/shuaishuai80/article/details/6140979?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-4.control&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-4.control)