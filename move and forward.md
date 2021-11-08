# move and forward

```c++
template <typename T>
typename remove_reference<T>::type&& move(T&& t)
{
	return static_cast<typename remove_reference<T>::type&&>(t);
```

无名的右值引用是右值
具名的右值引用是左值

[std::move和std::forward源码分析](https://blog.csdn.net/zwvista/article/details/6848582?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-3.control&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-3.control)