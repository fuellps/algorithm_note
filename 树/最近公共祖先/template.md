### 倍增法求最近公共祖先

- 对于节点x,y的最近公共祖先,一种朴素的做法是假使x的深度$dx$小于y的深度$dy$,那么让y往上跳,一直到和x的深度相同.如果此时y等于x,那么x就是最近祖先.否则,让x,y同时往上跳,则第一个相同的就是最近公共祖先
- 上面的做法太慢了,每次查询都要*O*(n)的复杂度,这时可用倍增算法优化向上跳和找祖先的过程.
- 令$fa[i][j]表示i号点的第2^j个祖先$,分类讨论:
  - 如果$j==0$,那么i号点的祖先就是其父亲
  - 如果$j>0$,那么i号点的祖先就是第$fa[i][j-1]$号点的第$2^{j-1}个祖先$

```c++
const int N = 1e5 + 100;
const int M = 2e5 + 10;
int n, m;
using namespace std;
using ll = long long;

int h[N], e[N << 1], ne[N << 1], idx = 1; 
int fa[20][N], depth[N];

int bit_length(ll k) {
    int res = 0;
    while (k) {
        res++;
        k >>= 1;
    }
    return res;

}


void add(int u, int v) {
    e[idx] = v;
    ne[idx] = h[u];
    h[u] = idx++;
}


void dfs(int u, int f) {
    fa[0][u] = f;
    for (int i = h[u]; i; i = ne[i]) {
        int v = e[i];
        if (v != f) {//当v不是u的父节点时，更新子树深度
            depth[v] = depth[u] + 1;
            dfs(v, u);
        }
    }
}

int lca(int x, int y) {
    if (depth[x] < depth[y]) swap(x, y); //让x为更深的点
    int diff = depth[x] - depth[y];
    for (int i = 0; diff; i++, diff >>= 1) {//二进制分解往上跳，使得x和y等高。
        if (diff & 1) {
            x = fa[i][x];
        }
    }
    if (x == y) return x;//已经za
    for (int i = m - 1; i >= 0; i--) {
        if (fa[i][x] != fa[i][y]) {//从高处跳，只要不是同一个祖先,就跳.
            x = fa[i][x];
            y = fa[i][y];
        }
    }
    return fa[0][x];//最后再跳一步一定为最近公共祖先
}


```



