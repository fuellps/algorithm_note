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
// 实现单点修改,区间查询的树状数组 P3374
#include <bits/stdc++.h>
using namespace std;
const int N = 5e5 + 10;
int tree[N],n,m;
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
        i -= lowbit(i);
    }
    return ans;
}
int main(){
    cin >> n >> m;
    for(int i = 1; i <= n; i++){
        int v; cin >> v;
        add(i,v);
    }
    while(m--){
        int op,x,y;
        cin >> op >> x >> y;
        if(op == 1) add(x,y);
        else cout<< query(y) - query(x-1) << endl;
    }
    return 0;
}
```

#### 范围修改,单点查询

只需将维护原数组改为维护差分数组即可.

#### 范围修改,范围查询

$$
设a_i=\sum_{j=1}^{i}d_j,\\
则前缀和sum(a[:n])=\sum_{i=1}^{n}a_i=\sum_{i=1}^{n}\sum_{j=1}^{i}d_j
\\=d_1 + (d_1 + d_2) + (d_1 + d_2 +d_3) + ...+(d_1+...+d_n)\\
=n*d_1+(n-1)*d_2+(n-3)*d_3+...+(n-(n-1))d_n\\
=n*\sum_{i=1}^{n}d_i -\sum_{i=1}^{n}(i-1)*d_i\\
或\\
\sum_{i=1}^{n}a_i=\sum_{i=1}^{n}\sum_{j=1}^{i}d_j = \sum_{i=1}^{n}d_j*(n-i+1)=(n+1)*\sum_{i=1}^nd_i - \sum_{i=1}^nd_i*i
$$

因此,可以用一个树状数组维护差分数组$d_i$,以及一个树状数组维护$(i-1)*d_i$.

或者维护差分数组$d_i$,以及一个树状数组维护$i*d_i$.
### 二维树状数组

#### 矩阵单点修改,区间查询

> [308. 二维区域和检索 - 可变](https://leetcode.cn/problems/range-sum-query-2d-mutable/) 题意:实现一个类,支持如下操作:
>
> 1.查询(row1,col1,row2,col2)的元素和
>
> 2.将(row,col)的值修改为val.

### Trick

#### 建树

> 一维O(n)建树:先求儿子,再更新父亲

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

- [P3374 【模板】树状数组 1](https://www.luogu.com.cn/problem/P3374)
- [P3368 【模板】树状数组 2](https://www.luogu.com.cn/problem/P3368#submit)

- [P3372 【模板】线段树 1](https://www.luogu.com.cn/problem/P3372) 
- [308. 二维区域和检索 - 可变](https://leetcode.cn/problems/range-sum-query-2d-mutable/) (会员题)