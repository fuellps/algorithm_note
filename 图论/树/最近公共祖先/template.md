### 倍增法求最近公共祖先

- 对于节点x,y的最近公共祖先,一种朴素的做法是假使x的深度$dx$小于y的深度$dy$,那么让y往上跳,一直到和x的深度相同.如果此时y等于x,那么x就是最近祖先.否则,让x,y同时往上跳,则第一个相同的就是最近公共祖先
- 上面的做法太慢了,每次查询都要*O*(n)的复杂度,这时可用倍增算法优化向上跳和找祖先的过程.
- 令$fa[i][j]表示i号点的第2^j个祖先$,分类讨论:
  - 如果$j==0$,那么i号点的祖先就是其父亲
  - 如果$j>0$,那么i号点的祖先就是第$fa[i][j-1]$号点的第$2^{j-1}个祖先$

```c++
int fa[N][20]; //第二维的范围为logn取上整
int depth[N];
// 求深度同时预处理f[i][0]
int dfs(u,fa){
    fa[u][0] = f;
    for (int v : g[u]){ //假使用vector存储邻接表
        if (v != f){
            depth[v] = depth[u] + 1;
            dfs(v,u);          
        }
    }
}

//倍增预处理祖先
for(int j = 1; 1<< j <= n; j++){
    for(int i = 1; i <= n; i++){
        fa[i][j] = fa[fa[i][j-1]][j-1];
    }
}

while (q--){ #假使q组询问x,y的最近公共祖先
   cin >> x >> y;
   if(depth[x] > depth[y]) swap(x,y);
   int diff = depth[y] - depth[x];
   // 2进制分解,加速向上跳
   for(int i = 0;1<<i <= diff; i++){
       if(diff>>i&1){
           y = fa[y][i];
       }
   }
    // 向上跳完和x同一深度,x为最近公共祖先
   if(y == x){ 
       cout << x << endl;
       continue;
   }
  //查找最近公共祖先
   for(int i = 20; i >= 0;i--){
       if(fa[x][i] != fa[y][i]){
           x = fa[x][i];
           y = fa[y][i];
       }
   }
   cout << fa[x][0] << end
            
}
```



