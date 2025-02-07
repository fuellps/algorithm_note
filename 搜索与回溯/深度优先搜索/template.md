### 深度优先搜索DFS

深度优先搜索应用非常广泛,广泛用于遍历树,图等结构,借助递归无需手动维护栈,代码量小.

### 模板一:子集枚举

> 给定整数数组$[a_0,a_1...a_{n-1}]$,求所有的子集(即幂集).
>
> 例如给定数组[1,2,3],则结果为[],[3],[2],[2,3],[1],[1,3],[1,2],[1,2,3]

> 有两种做法:
>
> ①:使用递归搜索.

```c++
vector<int> path;
// dfs(i)表示当前选择到第i个下标
void dfs(i){
    if(i == n){
        for (int x : path){
			cout << x << " ";
        }
        cout << end;
        return;
    }
    dfs(i+1); // 不选下标为i个数
    path.push_back(nums[i]); // 选下标为i个数
    dfs(i+1);
    path.pop_back();
}
```

> ②:二进制枚举:每个32/64位整数,可以看作是大小为32/64长度的集合.如果某位上为1,则代表存在(选),为0代表不存在(不选)

```c++
for(int i  =0;i < 1 << n; i++){
    for (int j  = 0;j < n; j++){
        if(i>>j&1){
			cout << nums[i] << " ";
        }
    }
    cout << endl;
}
```



### 模板二:全排列

> 给定整数数组$[a_0,a_1...a_{n-1}]$,求所有的排列.
>
> 例如给定数组[1,2,3],则结果为[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]

> 有两种做法.
>
> ①:每次交换相邻的两个数.$致命缺点:不能按照字典序递增的顺序枚举,且必须要枚举全部的排列,不能从某个排列开始枚举$

```c++
void permutation(int i,int* nums){
    if(i == n){
        for(int j = 0;j < n; j++) cout << nums[i] << " ";
        cout << endl;
    }
    for(int j  = i;j < n; j++){
        swap(nums[i],nums[j]); //保护现场
        permutation(i+1,nums);
        swap(nums[i],nums[j]); // 还原现场
    }
}
```

> ②用一个数组vis标记选了哪些数字,按照字典序的顺序枚举即可得到按字典序递增的排列

```c++
vector<int> path(N);
void permutation(int i,int* nums){
    if(i == n){
        for(int j = 0;j < n; j++) cout << path[i] << " ";
        cout << endl;
    }
    for(int j  = 0;j < n; j++){
        if(!vis[j]){
            vis[j] = true;
            path[i] = nums[j]; 
            permutation(i+1,nums);
            vis[j] = false; #path可以不用还原现场,因为每次递归都被覆盖了,就相当于还
        }
    }
}
```

