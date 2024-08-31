kruskal算法流程为先对边按照边权排序,然后判断最小边的两个端点是否在同一集合内,如果不在的话就合并两个点,找到一条边.

```c++
#include <bits/stdc++.h>
using namespace std;
const int N = 100010,M=200010;
int n,m,fa[N];
struct node{
    int u,v,w;
}edge[M];
int find(int x){
    return x == fa[x] ? x : fa[x] = find(fa[x]);
}
#define INF 0x3f3f3f3f
bool cmp(node &aa,node &bb){
//    return aa.w - bb.w;//Error
    return  aa.w < bb.w;//比较函数,注意返回的是bool,而不是整数类型
}
int kruskal(){
    sort(edge,edge+m,cmp);
    
    int res = 0,cnt = 0;
    for(int i = 0; i < m; i++){
        int a = find(edge[i].u),b = find(edge[i].v);
        if(a != b){//两个点不在同一集合,找到一条合法的bian
            fa[a] = b;
            res += edge[i].w;
            cnt++;
        }
    }
    return cnt == n-1 ? res : INF;
}
int main()
{
    cin >> n >> m;
    for(int i= 0; i < m; i++){
        cin >> edge[i].u >> edge[i].v >> edge[i].w;
    }
    for(int i = 1; i <= n; i++){
        fa[i] = i;
    }
    int d = kruskal();
    if(d == INF) cout <<"impossible";
    else cout <<d;
}
```

