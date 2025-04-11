[toc]



## 模板

### 一维树状数组

#### 单点修改,区间查询

树状数组是一种支持**单点修改**和**范围查询**的代码量小的一种数据结构.

> 普通树状数组维护的信息及运算要满足 **结合律** 且 **可差分**，如加法（和）、乘法（积）、异或等。

![img](template.assets/fenwick.svg)

- 对于树状数组第i个数,管辖的区间长度为lowbit(i),范围为[i-lowbit(i) + 1,i]
- 区间查询时,每次跳lowbit(i)个单位,能将前缀不重不漏拆分.
- 单点修改时,每次跳lowbit(i)个单位

```c++
inline int lowbit(int x){
    return x&-x;
}
// 单点修改
void add(int i,int v){
    while(i <= n){
        tree[i] += v;
        i += lowbit(i);
    }
}
// 范围(前缀)查询
int query(int i){
    int ans = 0;
    while(i){
        ans += tree[i];
        i -= lowbit(i); //等价于 i&=i-1
    }
    return ans;
}
//建树  O(nlogn)
void build(int n){
    for(int i = 1; i <= n; i++) add(i,a[i]);
}
/*
操作1：将第x个数加上y
add(x,y);
操作2：查询[x,y]的区间和
query(y) - query(x-1);
*/
```

#### 范围修改,单点查询

只需将维护原数组改为维护差分数组即可.

#### 范围修改,范围查询

> 该问题可以使用两个树状数组维护差分数组解决。

$$
\begin{aligned}
&首先考虑如何查询区间[1,r]的前缀和 \\
&设a_i=\sum_{j=1}^{i}d_j,其中d_i = a[i]-a[i-1] \\
&则前缀和sum(a[1:r])=\sum_{i=1}^{r}a_i=\sum_{i=1}^{r}\sum_{j=1}^{i}d_j\\
&=d_1 + (d_{1} + d_{2})  + ...+(d_1+...+d_r)\\
&=r*d_1+(r-1)*d_{2}+...+(r-(r-1))d_r\\
&=r*\sum_{i=1}^{r}d_i -\sum_{i=1}^{r}(i-1)*d_i\\
&或者\\
&\sum_{i=1}^{r}a_i=\sum_{i=1}^{r}\sum_{j=1}^{i}d_j = \sum_{i=1}^{r}d_j*(r-i+1)= (r+1)*\sum_{i=1}^rd_i - \sum_{i=1}^rd_i*i
\end{aligned}
$$

因此,可以用一个树状数组维护差分数组$d_i$,以及一个树状数组维护$(i-1)*d_i$.

或者维护差分数组$d_i$,以及一个树状数组维护$i*d_i$.

> 还有一个问题，就是如何维护区间加法呢？

$$
\begin{aligned}
&考虑a[l:r]区间加x给d带来的影响	\\
&对于d[l],由于a[l]多加x，而a[l-1]没有加x，因此d[l]多加了x \\
&对于d[r],由于a[r]多加x，而a[r+1]不变，因此d[r+1]多减了x \\
&对于 l < i < r,由于d[i] = a[i] - a[i-1]，同时a[i],a[i-1]都加上x因此d[i]不变 \\
&所以对于维护d_i的树状数组，对l单点加v，对r+1单点加-v; \\
&对于维护i*d_i的树状数组，对l单点加l*v,对r+1单点加-(r+1)*v
\end{aligned}
$$

代码示例：

```c++
using ll = long long;

ll lowbit(ll x) { return x & -x; }

void update(int x, ll v) {
    ll v2 = x*v;
    while (x <= n) {
        tree1[x] += v;
        tree2[x] += v2;
        x = x + lowbit(x);
    }
}

ll query(ll* tree,ll x) {
    ll ans = 0;
    while (x) {
        ans += tree[x];
        x -= lowbit(x);
    }
    return ans;
}
//建树
void build(int n) {
    for (int i = 1; i <= n; i++) {
        update(i,a[i]);
        update(i+1,-a[i]);
    }
}
//查询区间和
ll get_sum(int l,int r){
    return (r+1)* query(tree1,r) - query(tree2,r) +  query(tree2,l-1) - l*query(tree1,l-1);
}

/*
操作1：将a[x:y] +k 
update(x,k);
update(y+1,-k);
操作2： 查询sum(a[x:y])
get_sum(x,y)
*/
```



### 二维树状数组

> 二维树状数组维护的和二维前缀和的定义是一样的

#### 矩阵单点修改,子矩阵查询

```c++
//单点加的模板
void add(int x,int y,int v){
    for(int i = x;i <= n; i+= lowbit(i)){
        for(int j = y; j <= m; j+= lowbit(j)){
            c[i][j] += v;
        }
    }
}

//【1，1】到【x,y】的和
int sum(int x,int y){
    int res = 0;
    for(int i = x; i; i -= lowbit(i)){
        for(int j = y; j; j -= lowbit(j)){
            res += c[i][j];
        }
    }
    return res;
}
//查询(x1,y1)到（x2,y2)的子矩阵和
int query(int x1,int y1,int x2,int y2){
    return sum(x2,y2) - sum(x1-1,y2) - sum(x2,y1-1) + sum(x1-1,y1-1);
}
//建树
void build(int n,int m){
    for(int i =1;i <= n; i++){
        for(int j = 1;j <= m; j++){
            add(i,j,g[i][j]);
        }
    }
}
```



> [308. 二维区域和检索 - 可变](https://leetcode.cn/problems/range-sum-query-2d-mutable/) 题意:实现一个类,支持如下操作:
>
> 1.查询(row1,col1,row2,col2)的元素和
>
> 2.将(row,col)的值修改为val.

#### 子矩阵修改,子矩阵查询

对于子矩阵修改,需要用到二维差分数组.假使`d[i][j]`为`a[i][j]`的差分数组.则

对于点`(x,y)`，它的二维前缀和可以表示为 $\sum_{i=1}^{n}\sum_{j=1}^{m}\sum_{x=1}^{i}\sum_{y=1}^{j}d[i][j]$,和一维数组数组【区间加，区间查询】类似，统计 `d(a,b)`出现的次数，为 $(x-a+1)*(y-b+1)$。
$$
\begin{aligned}
&\sum_{i=1}^{n}\sum_{j=1}^{m}a[i][j] = \sum_{i=1}^{n}\sum_{j=1}^{m}\sum_{x=1}^{i}\sum_{y=1}^{j}d[i][j]\\
&=\sum_{i=1}^{n}\sum_{j=1}^{m}d[i][j]*(n-i+1)*(m-j+1)\\
&=\sum_{i=1}^{n}\sum_{j=1}^{m}d[i][j]*(n+1)*(m+1) - d[i][j]*(n+1)*j\\
&-d[i][j]*(m+1)*i + i*j*d[i][j]\\
&=(n+1)*(m+1)\sum_{i=1}^{n}\sum_{j=1}^{m}d[i][j]-(n+1)\sum_{i=1}^{n}\sum_{j=1}^{m}d[i][j]*j\\
&-(m+1)\sum_{i=1}^{n}\sum_{j=1}^{m}d[i][j]*i+\sum_{i=1}^{n}\sum_{j=1}^{m}i*j*d[i][j]

\end{aligned}
$$
因此,可以用四个二维树状数组维护

$\sum_{i=1}^{n}\sum_{j=1}^{m}i*j*d[i][j]$,

$\sum_{i=1}^{n}\sum_{j=1}^{m}d[i][j]*j$,

$\sum_{i=1}^{n}\sum_{j=1}^{m}d[i][j]*i$,

$\sum_{i=1}^{n}\sum_{j=1}^{m}d[i][j]$

模板:[P4514 上帝造题的七分钟](https://www.luogu.com.cn/problem/P4514)

```c++
#include<bits/stdc++.h>
using namespace std;
const int N = 2100;
int tree1[N][N],tree2[N][N],tree3[N][N],tree4[N][N],n,m;
int lowbit(int x){return x&-x;}
//tree1-> d[i][j],tree2->i*d[i][j],tree3->j*d[i][j],tree4->i*j*d[i][j]
void add(int x,int y,int v){
    int v1=v,v2=v*x,v3=v*y,v4=x*y*v;
    for(int i  = x;i <= n; i += lowbit(i)){
        for(int j = y; j <= n; j += lowbit(j)){
            tree1[i][j] += v1;
            tree2[i][j] += v2;
            tree3[i][j] += v3;
            tree4[i][j] += v4;
        }
    }
}
// 二维前缀和
int sum(int x,int y){
    int ans=  0;
    for(int i = x; i; i -= lowbit(i)){
        for(int j = y; j; j -= lowbit(j)){
            ans += (x+1)*(y+1)*tree1[i][j] - (y+1)*tree2[i][j]
            - (x+1)*tree3[i][j] + tree4[i][j];
        }
    }
    return ans;
}
// 二维差分
void update(int x1,int y1,int x2,int y2,int v){
    add(x1,y1,v);
    add(x1,y2+1,-v);
    add(x2+1,y1,-v);
    add(x2+1,y2+1,v);
}
int main(){
    char op;
    cin >> op >> n >> m;
    int x1,y1,x2,y2,v;
    while(cin >> op){
        if(op == 'L'){
            cin >> x1 >> y1 >> x2 >> y2 >> v;
            update(x1,y1,x2,y2,v);
        }else{
            cin >> x1 >> y1 >> x2 >> y2;
            // z
            cout << sum(x2,y2) - sum(x2,y1-1) - sum(x1-1,y2) + sum(x1-1,y1-1) <<endl;
        }
    }
    return 0;
}
```



### Trick

#### 建树

> 一维O(n)建树:每一个节点的值是由所有与自己直接相连的儿子的值求和得到的。因此可以倒着考虑贡献，即每次确定完儿子的值后，用自己的值更新自己的直接父亲。

```c++
    for(int i = 1; i <= n; i++){
        tree[i] += a[i];
        int j = i + lowbit(i);
        if(j <= n) tree[j] += tree[i];
    }
```

> 二维O(n^2)建树:先进行第二维,后进行第一维.

```c++
//二维树状数组O(n^2)建树
         for(int i = 1; i <= n; i++){
            for(int j = 1;j <= m; j++){
                tree[i][j] += matrix[i][j];
                int jj = j  + lowbit(j);
                if(jj <= m){
                    tree[i][jj] += tree[i][j];
                }
            }
         }
         for(int i = 1; i <= n; i++){
            for(int j = 1;j <= m; j++){
                int ii = i  + lowbit(i);
                if(ii <= n){
                    tree[ii][j] += tree[i][j+];
                }
            }
         }
```



### 题目练习

#### 模板

- [树状数组 1：单点修改，区间查询](https://loj.ac/problem/130)
- [树状数组 2：区间修改，单点查询](https://loj.ac/problem/131)
- [树状数组 3：区间修改，区间查询](https://loj.ac/problem/132)
- [二维树状数组 1：单点修改，区间查询](https://loj.ac/problem/133)
- [二维树状数组 2：区间修改，单点查询](https://loj.ac/problem/134)
- [二维树状数组 3：区间修改，区间查询](https://loj.ac/problem/135)
- [308. 二维区域和检索 - 可变](https://leetcode.cn/problems/range-sum-query-2d-mutable/) (会员题) 单点修改，子矩阵查询

#### 题目

> 下面习题基本都可用线段树解决。

- [315. Count of Smaller Numbers After Self](https://leetcode.cn/problems/count-of-smaller-numbers-after-self/) 逆序对 
- [Luogu P1966  火柴排队](https://www.luogu.com.cn/problem/P1966) `经典习题`
- 

