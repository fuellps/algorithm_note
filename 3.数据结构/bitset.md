### C++中的bitset

##### 声明

```c++
bitset<10000> bit;//指定大小
```

##### 构造函数

```c++
bitset()//每一位都为false
bitset(unsigned long val)
bitset(const string& str)
```

##### 成员函数

```c++
count() //返回集合中为true的数量（1的个数）
_Find_first()://返回bitset第一个true的下标,若没有true则返回bitset的大小。其实就是集合大小
```





### 习题练习

- [[蓝桥杯 2021 省 AB\] 砝码称重](https://www.luogu.com.cn/problem/P8742)
- [划分](https://www.lanqiao.cn/problems/17143/learning/?page=1&first_category_id=1&name=%E5%88%92%E5%88%86)
- [[NOIP 2002 普及组\] 产生数](https://www.luogu.com.cn/problem/P1037)