floyd算法可求出所有点之间的最短路

f\[k]\[i][j] 表示在考虑了k号点后,i号点到j号点的最短距离

则f\[k]\[i][j] = min(f\[k-1]\[i][j],f\[k-1]\[i][k] + f\[k-1]\[k][j])不考虑k号点的最短路和考虑k号点的最短路

由于f[k]只由f[k-1]转移而来,因此可以省略一维数组.用二维数组代替即可.

```c++
#include <bits/stdc++.h>
using namespace std;
const int N = 210;
int g[N][N],n,m,k,x,y,u,v,w;


void floyd(){
    //O(n^3)三重for循环
    for(int k = 1; k <= n; k++){
        for(int i =1; i <= n; i++){
            for(int j = 1; j <= n; j++){
                g[i][j] = min(g[i][j], g[i][k] + g[k][j]);
            }
        }
    }
}
int main(){
    cin >> n >> m >> k;
    for(int i = 1; i <= n; i++){
        for(int j = 1; j <= n; j++){
            if(i == j) g[i][j] = 0; //由于询问任意两个点的距离,可能询问同一个点,所以要初始化为0
            else g[i][j] = 0x3f3f3f3f;
        }
    }
    // memset(g,0x3f, sizeof g);
    for(int i = 0; i < m; i++){
        cin >> u >> v >> w;
        g[u][v] = min(g[u][v],w);
    }
    floyd();
    while(k--){
        cin >> x >> y;
        if(g[x][y] > 0x3f3f3f3f/2) cout << "impossible" <<endl;
        else cout << g[x][y]<<endl;
    }
}
```

