### 倍增

对于一个查询，我们如果我们可以先预处理处所有可能的情况执行一次操作后的值，我们就能根据先前预处理的值成2倍增长进行计算。 



### st表

ST表适用于**区间可重复贡献**的查询问题.比如说查询区间的最小值,最大值,GCD,区间或,区间与等.

以求区间最大值为例:

#### 预处理出$f[i][j]$的值

$$
\begin{aligned}
&定义f[i][j]表示从i位置开始的2^j个元素的最大值,即f[i][j] = [i,i + 2^j - 1] \\
&显然有对于j = 0,有\sum_{i=0}^n f[i][i] = a[i] \\
&对于j > 0,考虑如何转移:此时已经知道了位置i后的的2^{j-1}个元素 \\
&则可以通过f[i][j] = f[i][j-1] + f[i +2^{j-1}][j-1]转移而来 \\
\end{aligned}
$$

#### 区间查询

预处理出$f[i][j]$后考虑如何回答[l,r]区间的最大值.
$$
\begin{aligned}
&考虑左端点l,求区间[l,l+2^x-1]最大值 \\
&考虑右端点r,求f[r-2^x + 1,r]最大值 \\
&当x取\lfloor log(r-l + 1) \rfloor可以覆盖到所求的区间区间 \\
&即满足 l+2^r-1 \ge r-2^x + 1
\end{aligned}
$$

证明如下:

$$
\begin{aligned}
&设k=r-l+1,p= \lfloor \log k \rfloor \\
&则有2^{p} \le k \lt 2^{p+1}\\
&\therefore k \le 2^{p+1} -1\qquad (k为整数) \\
&考虑反证法:假设 l+2^p-1 \lt r-2^p + 1 \\
&则有 2^{p+1} - 1\lt k \\
&与上面推出的结论相反,不成立. \\
&所以有l+2^p-1 \ge r-2^p + 1
\end{aligned}
$$



代码实现时可以先预处理log的值.
$$
\begin{equation}
Log\lfloor i \rfloor = 
\begin{cases}
 0&\mbox{i = 1} \\
 Log\lfloor i/2 \rfloor + 1& \mbox{i > 1}
\end{cases}
\end{equation}
$$

```c++
const int logn = 20;//2^20 > 1e6
const int N = 1e5 + 10;
int f[N][logn]; //ST表
int Log[N]; //logX的值

//预处理ST表
// f[i][j] = max(f[i][j-1], f[i + 2^{j-1}][j-1]
//BASE:
for(int i = 1; i <= n; i++) f[i][0] = a[i];

for(int j = 1; j <= logn; j++){
    for(int i = 1;i + (1<<j) - 1 <= n; i++){
        f[i][j] = max(f[i][j-1], f[i + (1 << j - 1)][j-1]);
    }
}

//预处理Log
//BASE:
// Log[1] = 0;
// Log[i] = Log[i/2] + 1
for(int i = 2;i <= n; i++){
    Log[i] = Log[i/2] + 1;
}

//处理查询
while(q--){
    int l,r;
    cin >> l >> r;
    int x = Log[r - l + 1];
    cout << max(f[l][x], f[r - (1<<x) + 1][x]);
}
```





### 习题练习

- https://www.luogu.com.cn/problem/P2880 `st表模板题.求区间最大值和最小值`
- https://www.luogu.com.cn/problem/P1890 `区间gcd.数据量比较水.`

- [如今仍是遥远的理想之城1 ](https://www.lanqiao.cn/courses/21968/learning/?id=1623008&compatibility=false) `第i个传送阵能传送到a[i]处，从1号出发，问执行k次能传送到的位置.课程。` 
- [数的变换](https://www.lanqiao.cn/courses/21968/learning/?id=1623009&compatibility=false) `每次操作能将A=[A/B] + c,问执行k次操作后A的值.` `课程`
- https://www.luogu.com.cn/problem/P4155 `国旗计划.破环成链技巧+倍增优化.`
- https://vjudge.net/problem/UVA-11235 `求有序数组中[l,r]出现的众数数量.`
- 
