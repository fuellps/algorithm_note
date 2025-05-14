```c++
//在下面的内建函数后缀加上ll，则表示(unsigned) long long类型。
cout << __builtin_ffs(10) << endl; //1010 返回第1位的位置
//output: 2
cout << __builtin_clzll(16) << endl;//1 0000  64-5=59.返回前导0的个数
//output: 59
cout << __builtin_ctz(16) << endl; //1 0000 返回尾部0的个数
//output: 4
cout << __builtin_popcount(16) << endl;//1 0000 返回1的个数
//output: 1
```

