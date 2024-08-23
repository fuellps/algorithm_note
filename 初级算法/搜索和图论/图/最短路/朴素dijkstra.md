初始化集合{s}为空中,遍历n-1次,每次从不在s中取出距离源点最短距离的点,更新该点到其他点的最短距离,并将该点加入集合{s}中.

```c++
#include <bits/stdc++.h>
using namespace std;
const int N = 510;
int g[N][N],dis[N],n,m;
bool vi[N];
int dijkstra()  // 求1号点到n号点的最短路距离，如果从1号点无法走到n号点则返回-1
{
    memset(dis, 0x3f, sizeof dis);
    dis[1] = 0;
    for(int i = 1; i < n; i++){//只需遍历n-1个点,每次更新的点的距离都是最小的,剩下一个点肯定无法更新其他点
        int t = -1;
        for(int j = 1; j <= n; j++){
            //从未在s的集合中找到距离源点最近的点
            if(!vi[j] && (t == -1 || dis[t] > dis[j])){
                t = j;
            }
        }
        vi[t] = true;//将该点加入集合中
        for(int j = 1;j <= n; j++){// 更新该点到其他点的最短距离
            dis[j] = min(dis[j],dis[t] + g[t][j]);
        }
    }
    //1号点到n号点距离不为最大值,说明两点间存在通路,否则不存在通路
    return dis[n] != 0x3f3f3f3f ? dis[n] : -1;
}

int main()
{
    cin >> n >> m;
    memset(g, 0x3f, sizeof g);//由于都是正权边,因此自环并不会影响答案,因为最短路不可能会绕圈走环.所以这题可以直接全部初始化邻接矩阵为最大值
    for(int i = 0; i < m; i++){
        int u,v,w;cin >> u >> v >> w;
        g[u][v] = min(g[u][v],w);
    }
    cout << dijkstra();
}
```

