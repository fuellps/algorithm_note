ST表适用于区间可重叠的查询问题.比如说查询区间的最小值,最大值,GCD等.

以求区间最大值为例:

#### 预处理出$f[i][j]$的值

定义$f[i][j]表示从i开始,后2^j个元素的最大值,即f[i][j] = [i,i + 2^j - 1]$

显然有$对于j = 0,有\sum_{i=0}^n f[i][i] = a[i]$

$对于j > 0,考虑如何转移:此时已经知道了位置i后的的2^{j-1}个元素$

$则可以通过f[i][j] = f[i][j-1] + f[i +2^{j-1}][j-1]转移而来$

$对于每个确定的j,i的范围需要满足i +2^j - 1 <= n$

#### 区间查询

预处理出$f[i][j]$后考虑如何回答[l,r]区间的最大值.

考虑左端点l,$求区间[l,l+2^r-1]最大值$

考虑右端点r,$求f[r-2^x + 1,r]最大值$

当x取$\lfloor log(r-l + 1) \rfloor可以覆盖到所求的区间区间$

$令r-2^x+1 <= l + 2^x - 1,则有2^{x+1} >= r - l + 2,\\即x + 1 >=\lfloor log(r-l+2) \rfloor \\x >=\lfloor log(r-l+2)-1 \rfloor \\ x >= \lfloor log[(r-l+2)/2] \rfloor$

由于$log(r-l+1) = log(r -l + r - l+2)/2 >= log(r-l+2)/2当前仅当l = r时等号成立$



代码实现时可以先预处理log的值.
$$
\begin{equation}
Log[i] = 
\begin{cases}
 1&\mbox{i = 1} \\
 Log[i/2] + 1& \mbox{i > 1}
\end{cases}
\end{equation}
$$

```c++
const int logn = 20;
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
Log[1] = 0;
// Log[i] = Log[i/2] + 1
for(int i = 2;i <= n; i++){
    Log[i] = Log[i/2] + 1;
}

//处理查询
while(q--){
    int l,r;
    cin >> l >> r;
    int x = Log[r - l + 1];
    cout << max(f[l][x], f[r - (1<<x) + 1][x])
}
```

