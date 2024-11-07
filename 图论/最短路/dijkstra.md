> dijkstra算法是一种单源最短路算法.(从1个点出发,到达其他顶点的最短距离.)dijkstra利用贪心的思路,从源点出发,每次选取已确定的点中距离源点最近的点,然后以该点去更新到周围顶点的距离.后面就不再访问该点,因为该点到源点的最近距离已经确定了.
>
> dijkstra算法必须保证图中没有负权边,因此每次都是贪心的选取当前已确定的距离最小的点,如果后面有负权边,可能会导致更新不到,出现错误.
>
> dijkstra算法最多只需遍历|V|-1次,因为图中都是正权边,最短路不可能经过1个点两次,否则再经过一次只会使最短路权值变大.即最短路最多经过n-1条边.
>
> 
>
>  朴素版dijkstra算法(时间复杂度O($N^2$))

```java
int[][] g; //邻接矩阵,存储图之间的关系 (如果不存在边的话,初始化较大的常数)
int[] d; //存储源点到其他点的最短距离
boolean[] used;
int n,m; //n表示顶点数,m表示边数
//求顶点u到顶点v的最短距离
int  dijkstra(int u,int v){
    //点的编号从0到n-1
    Arrays.fill(d,Integer.MAX_VALUE/2); //不要初始化为最大值,后面会更新所有点一次
    d[u] = 0;
    for(int i = 0;i < n - 1; i++){//遍历|V|-1条边即可
        int  t = -1;
        for(int j = 0;j < n; j++){
            //找到未访问过且距离源点最近的点
            if(!used[j] && (t == -1 || d[j] < d[t])){
                t = j;
            }
        }
   //     if(t == v) return d[v]; 可以提前剪枝
		if(t < 0) break; //没有点可以更新了
        for(int j = 0;j < n; j++){
            //有边相连且能够更新
            if(g[t][j] != Integer.MAX_VALUE &&d[t] + g[t][j] < d[j]){
                d[j] = d[t] + g[t][j];
            }
        }
    }
    
    //此时源点到所有顶点的最近距离已经求出,如果图不连通,则有些距离仍为inf
    
}
```

$注意事项:注意题目描述有没有重边和自环.如果有重边和自环的话,每次新加边需要和原来的值取一个最小值$

$朴素版dijkstra即使图没有和源点连通的话,也会更新点,所以距离不要初始化为最大值,防止溢出$





>  朴素版dijkstra在查找距离源点最近的点需要花费O(n)的时间,因此整体复杂度为O(n^2)
>
> 而快速找出最小值这个操作可以用堆(优先队列)进行优化.这样图可以用邻接表进行存储.时间复杂度可以优化到O(|E|*log|E|) 
>
> log|E|是因为一个点的到源点的最短路可能被多个点更新,因此**堆中可能会有重复的元素**.堆中元素的数量级大约是边数的规模.

```java
class Solution {
    //链式前向星建图
    static int N = 101;
    static int M = 6001;
    static int[] h = new int[N],ne = new int[M],e = new int[M],w = new int[M];

    static int idx;
    static void add(int u,int v,int c){
        e[idx] = v;
        w[idx] = c;
        ne[idx] = h[u];
        h[u] = idx++;
    }
    static void init(){
          Arrays.fill(h,0);
          idx = 1;
    }
    public int networkDelayTime(int[][] times, int n, int k) {
        init();
        for(int[] e : times){
            add(e[0],e[1],e[2]);
        }
        //优先队列
        PriorityQueue<int[]> q = new PriorityQueue<>((a,b) -> a[0] - b[0]);
        int[] d = new int[n+1];//源点到其他点的最近距离
        Arrays.fill(d,Integer.MAX_VALUE);
        d[k] = 0;
        q.add(new int[]{0,k});
        while(!q.isEmpty()){
            int[] m = q.poll();
            int u = m[1],c = m[0];
            if(c > d[u]) continue; //该点最近距离已经确定
            for(int i  = h[u]; i != 0;i = ne[i]){
                int v = e[i];
                if(d[u] + w[i]  < d[v]){
                    d[v] = d[u] + w[i];
                    q.add(new int[]{d[v],v});
                }
            }
        }
        //此时源点到其他点的最近距离已经确定了
        int ans = 0;
        for(int i = 1; i <= n; i++){
            if(d[i] == Integer.MAX_VALUE) return -1;
            ans = Math.max(ans,d[i]);
        }
        return ans;
    }
}
```

