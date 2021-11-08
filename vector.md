# vector

1. shrink_to_fit() :将capacity()减少到和size()相同大小。  搭配clear()使用，可以清空vector所占内存。

2. reserve(n):分配至少容纳n个元素的内存空间。假设当前size()==24， capacity()==32,调用reserve(50)就会使capacity()大于等于50；此时容器最多能容纳大于等于50个元素。如果再占满，添加新元素时，就需要两倍内存分配策略。size()+1，capacity()翻倍！

3. size():指当前已经保存的元素数目

4. capacity(): 指在不分配新内存空间的情况下，容器最多能容纳的元素个数。每次在添加新元素时，都以capacity()分配策略往上分配，一般新空间内存大小是当前元素个数的两倍。
5. clear():清除内容
6. vector<T>().swap(Jwait):释放空间