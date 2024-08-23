spfa求负环的方法有两种:一:求出每个点入队的次数,如果某个点的入队次数等于n,说明有负环.

二:统计当前每个点的最短路所包含的边数,如果某个点的最短路所包含的边数大于等于n,则说明存在负环.

一般采用第二种方法.初始时将所有点加入队列.

可以按照这样来理解:在图中新建一个虚拟的超级源点,虚拟源点到所有点的距离都为0.第一次更新时会更新所有点的距离,因此会将所有点加入队列中.

求图中是否存在负环,等价于在新图中求是否存在负环.

```c++
#include <bits/stdc++.h>
using namespace std;
const int N = 2010,M=10010;
int head[N],e[M],ne[M],w[M],idx = 1;
int dis[N],//所有点到虚拟源点的距离
cnt[N];//cnt[i]表示经过多少条边更新成dis[i].
int n,m;
bool vi[N];
void add(int u,int v,int c){
    e[idx] = v,w[idx] = c,ne[idx] = head[u],head[u] = idx++;
}
bool spfa(){
    //所有点到虚拟源点的距离为0,不需要初始化
    queue<int> q;
    for(int i = 1; i <= n; i++){
        vi[i] = true;
        q.push(i);//将所有点都加入队列中,这样能判断整个图是否存在负环.
    }
    while(q.size()){
        int u = q.front();q.pop(); 
        vi[u] = false;//出队
        for(int i = head[u];i; i = ne[i]){
            if(dis[e[i]] > dis[u] + w[i]){
                dis[e[i]] = dis[u] + w[i];
                cnt[e[i]] = cnt[u] + 1;
                 if(cnt[u] >= n) return true; //有n条边更新,说明经过n+1个点,必然存在负环.
                if(!vi[e[i]]){
                     q.push(e[i]);
                     vi[e[i]] = true;
                }
            }
        }
    }
    return false;
}
int main(){
    cin >> n >> m;
    for(int i = 0; i < m; i++){
        int u,v,c;cin>>u>>v>>c;
        add(u,v,c);
    }
    cout << (spfa() ? "Yes" : "No") <<endl;
}
```

