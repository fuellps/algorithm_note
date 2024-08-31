朴素版prim就是维护一个集合{s},每次用图中找到与集合{s}距离最小的边,从边的一个点出发,去更新其他边.下次循环再找到与集合{s}距离最小的边,从边的一个点出发,继续更新.

```c++
#include <bits/stdc++.h>
using namespace std;
const int N = 510,INF = 0x3f3f3f3f;
int g[N][N],dis[N],n,m;
bool vi[N];

int prim(){
    memset(dis,0x3f,sizeof dis);//初始化距离数组
    int res = 0;//最小生成树的大小
    for(int i = 0;i < n; i++){
        int t = -1;
        for(int j = 1; j <= n; j++){//找到与集合s距离最短的边的点.
            if(!vi[j] && (t == -1 || dis[t] > dis[j])){
                t = j;
            }
        }
        if(i && dis[t] == INF) return INF; //如果不是第一次更新的点,说明这是距离集合最近的点,且该点距离为INF,说明与集合s不连通
        if(i) res += dis[t];//添加边权.注意要先加后更新,因为图中可能存在负环,二最小生成树是没有环的
        vi[t] = true;
        for(int j = 1; j <= n; j++){
            dis[j] = min(dis[j],g[t][j]);//更新到集合{s}
        }
    }
    return res;
}
int main(){
    cin >> n>> m;
    memset(g,0x3f,sizeof g);
    for(int i = 0; i< m; i++){
        int u,v,w;cin>>u>>v>>w;
        g[u][v] = g[v][u] = min(g[u][v], w);
    }
    int t = prim();
    if(t == INF) cout <<"impossible";
    else cout<<t;
}
```

