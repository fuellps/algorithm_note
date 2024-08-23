spfa是对bellman-ford的优化,用一个队列维护到源点距离变小的点,以该点来更新到其他点的距离.将更新后的点加入队列中.

```c++
#include <bits/stdc++.h>
using namespace std;
const int N = 100010;
int head[N],e[N],ne[N],w[N],idx = 1;
int dis[N],n,m;
bool vi[N];
void add(int u,int v,int c){
    e[idx] = v,w[idx] =c,ne[idx] = head[u],head[u] = idx++;
}
int spfa(){
    memset(dis,0x3f,sizeof dis);
    dis[1] = 0;
    queue<int> q;//存储的是所有到源点距离变小的点,以变小的点来更新其他点
    q.push(1);
    vi[1] = true;//表示当前在队列中的点
    while(q.size()){
        int u = q.front();q.pop();
        vi[u] = false;
        for(int i = head[u]; i; i = ne[i]){
            if( dis[e[i]] > dis[u] + w[i]){//能更新距离
                dis[e[i]] = dis[u] + w[i];
                if(!vi[e[i]]){//防止重复加入点,提高效率
                q.push(e[i]);
                vi[e[i]] = true;
                }
            }
        }
    }
    return dis[n];
}
int main()
{
    cin >> n >> m;
    for(int i = 0; i < m; i++){
        int u,v,c;cin>>u>>v>>c;
        add(u,v,c);
    }
    int d  = spfa();
    if(d == 0x3f3f3f3f) cout <<"impossible";
    else cout << d;
}
```

