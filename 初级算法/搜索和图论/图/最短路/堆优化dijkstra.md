朴素版的dijkstra每次都要花O(n)的时间去找到不在s中距离最近的点.而在一堆数中找到最小值可以用堆来进行优化.

```c++
#include <bits/stdc++.h>
using namespace std;
const int N = 150010;
int head[N],e[N],ne[N],w[N],idx = 1;
int n,m,u,v,c,d[N];
bool vi[N];
typedef pair<int,int> pII;
void add(int u,int v,int c){
    e[idx] = v,w[idx] = c,ne[idx] = head[u],head[u] = idx++;
}
#define x first
#define y second

int dijkstra(){
    memset(d,0x3f,sizeof d);
    d[1] = 0;
    priority_queue<pII,vector<pII>,greater<pII>> q;//小根堆写法,c++默认是大根堆
    q.push({0,1});
    while(q.size()){
        auto me = q.top();q.pop();
        u = me.y;c = me.x;
        if(u == n) break;
        if(vi[u]) continue;//每次更新距离就会加入1个点,最多会加入m个点,有可能会重复加点.
        vi[u] = true;
        for(int i = head[u]; i;i = ne[i]){
            if( d[e[i]] > c + w[i]){//如果能更新的话就更新.
                d[e[i]] = c + w[i];
                q.push({d[e[i]],e[i]});
            }
        }
    }
    return d[n] == 0x3f3f3f3f ? -1 : d[n];
}
int main(){
    cin >> n >> m;
    for(int i = 0; i < m; i++){
        cin >> u >> v >> c;
        add(u,v,c);
    }
   
    cout << dijkstra();
}
```

