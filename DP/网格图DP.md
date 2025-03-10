[toc]

## 前言

思考网格图DP时,一般是某个状态依赖于其他状态,且**该状态不论从哪里转移而来,对应的值是不会改变的.**


$$
一般来说,对于求min,max等问题的边界情况返回inf,-inf表示路径不合法\\

对于求路径方案数的问题,一般返回0,表示路径不合法
$$

## 基础:常见dp状态及空间优化



###  $一:两个数组滚动更新,这种做法比较通用$

$设状态方程为 dfs(i,j) = min(\sum_{k=0}^{m-1}dfs(i-1,k) + gird[i][j],dfs(i,j))$

```java
int[][] dp = new int[2][n];
for(int i = 0;i < n; i++){
    for(int j =0 ;j < m; j++){
        for(int k = 0;k < m; k++){
            dp[(i+1)&1][j+1] = Math.min(dp[i&1][k] + grid[i][j],dp[(i+1)&1][j+1])
        }
    }
}
```



### $二:一个数组滚动更新:一般依赖于上面一行或下面一行的几个状态$

$$
\begin{aligned}
&对于这种空间优化,一定要想清楚状态是依赖于原来的哪几个格子,第二层的遍历关系一般与依赖关系有关 \\
&如果依赖左边的格子,即已经在上一行的基础上计算好的本行结果,需要正序遍历.\\
&如果不依赖于在上一行计算好的本行结果,需要逆序遍历.
\end{aligned}
$$

**示例：**
$$
\begin{aligned}
&1.矩阵只允许向下或向右走.求从左上角到右下角的最大价值和. \\
&定义dfs(i,j)表示从(0,0)走到(i,j)的最大价值和 \\
&从(i,j)到(0,0)的最大价值和等于\quad max((i-1,j),(i,j-1)) + grid[i][j] \\
边界情况:&1.i < 0或者j<0,表示路径不合法,返回-inf,表示路径不合法.\\
&2.i=0,j=0,返回grid[0][0]表示路径合法 \\
\end{aligned}
$$

上述方程类似于完全背包，因此i,j正序遍历。

```java
//下面只给出空间优化后的代码
//每个状态只依赖于当前状态上面的格子,左边的格子.
//n = grid.length,m = gird[0].length
int[] dp = new int[m+1]; //向最左边一个状态,因此每个状态向右移动一位
Arrays.fill(dp,Integer.MIN_VALUE); //对于边界情况
for(int i = 0;i < n; i++){ //从底到顶,一步步推到记忆化搜索要求的状态
    for(int j = 0;j < m; j++){ //!!!每个格子依赖于左边的格子,必须从左往右遍历
        if(i == 0 && j== 0) dp[j+1] = grid[i][j];
        else dp[j+1] = Math.max(dp[j],dp[j+1]) + grid[i][j]; 
    }
}
return dp[m];
```

$2.矩阵允许向右,向下,向右下方向转移.求从左上角到右下角的方案数$

$子问题? 从dfs(i-1,j-1)或从dfs(i,j)或dfs(i-1,j+1)转移而来$

$当前子问题的答案? dfs(i,j) = dfs(i-1,j) + dfs(i,j+1) + dfs(i,j-1)$

$边界情况:1.i < 0或者j<0,表示路径不合法,返回0,表示路径不合法.\\2.i=0,j=0,返回1表示路径合法,找到一条路径$

```java
//每个状态只依赖于当前状态上面的格子,左边,左上方的格子.
//n = grid.length,m = gird[0].length
int[] dp = new int[m+1]; //向最左边一个状态,因此每个状态向右移动一位
//对于边界情况默认都是0,已经初始化完成
for(int i = 0;i < n; i++){ //从底到顶,一步步推到记忆化搜索要求的状态
    int prev = dp[0]; //或者prev = 0
    for(int j = 0;j < m; j++){//!!!每个格子依赖于左边的格子,必须从左往右遍历
        int t = dp[j+1] ; //记录下一成为左上角的状态
        if(i == 0 && j== 0) dp[j+1] = 1;
        else dp[j+1] += dp[j] + prev;
        prev = t; 
    }
}
return dp[m];
```



#### 网格图路径

以 [64. 最小路径和](https://leetcode.cn/problems/minimum-path-sum/)为例。动态规划求出对应的数组后只需从后往前递推即可。

```python
class Solution:
    def minPathSum(self, grid: List[List[int]]) -> int:
        path = []
        dp = [[inf]*(m+1) for _ in range(n+1)]
        for i in range(n):
            for j in range(m):
                if i == 0 and j == 0: dp[i+1][j+1] = grid[i][j]
                else:
                    dp[i+1][j+1] = min(dp[i][j+1],dp[i+1][j]) + grid[i][j]
        i,j = n,m
        # 注意先加答案，这样里面只需回溯到边界结束，不用在循环结束后在加上边界。
        path.append(grid[i-1][j-1]) #从最后一项开始往前回溯
        while i != 1 or j != 1:
            if dp[i][j] == dp[i-1][j] + grid[i-1][j-1]:
                i -= 1
            else:
                j -= 1
            path.append(grid[i-1][j-1])
        print(*reversed(path)) #由于是从后往前回溯，因此答案需要反转。
        return dp[n][m]
```



### 网格图练习习题:

#### 基础

-  [64. 最小路径和](https://leetcode.cn/problems/minimum-path-sum/)
-  [63. 不同路径 II](https://leetcode.cn/problems/unique-paths-ii/)
-  [120. 三角形最小路径和](https://leetcode.cn/problems/triangle/)
-   [931. 下降路径最小和](https://leetcode.cn/problems/minimum-falling-path-sum/) 1573
-   [2684. 矩阵中移动的最大次数](https://leetcode.cn/problems/maximum-number-of-moves-in-a-grid/) 1626     类似931，但稍微特别。
-    [329. 矩阵中的最长递增路径](https://leetcode.cn/problems/longest-increasing-path-in-a-matrix/)
-    [2328. 网格图中递增路径的数目](https://leetcode.cn/problems/number-of-increasing-paths-in-a-grid/) 2001
-   [2304. 网格中的最小路径代价](https://leetcode.cn/problems/minimum-path-cost-in-a-grid/) 1658
-   [1594. 矩阵的最大非负积](https://leetcode.cn/problems/maximum-non-negative-product-in-a-matrix/) 1807

> 同 [152. 乘积最大子数组](https://leetcode.cn/problems/maximum-product-subarray/)

-  [174. 地下城游戏](https://leetcode.cn/problems/dungeon-game/)  &#x1F60D;  `有助于更好理解动态规划`

#### 进阶

-  [3393. 统计异或值为给定值的路径数目](https://leetcode.cn/problems/count-paths-with-the-given-xor-value/) 1573  容易忽略情况 &#x1F60D; `多维`
-   [3418. 机器人可以获得的最大金币数](https://leetcode.cn/problems/maximum-amount-of-money-robot-can-earn/) 1798 多维 ·`做到空间优化`
-    [1301. 最大得分的路径数目](https://leetcode.cn/problems/number-of-paths-with-max-score/) 1853 &#x1F60D;  记录最大得分的路径及个数
-    [2435. 矩阵中和能被 K 整除的路径](https://leetcode.cn/problems/paths-in-matrix-whose-sum-is-divisible-by-k/) 1952
-    [2267. 检查是否有合法括号字符串路径](https://leetcode.cn/problems/check-if-there-is-a-valid-parentheses-string-path/) 2085  &#x1F60D;
-    [3363. 最多可收集的水果数目](https://leetcode.cn/problems/find-the-maximum-number-of-fruits-collected/) 实际难度 2200
-    [1463. 摘樱桃 II](https://leetcode.cn/problems/cherry-pickup-ii/)
-    [2510. 检查是否有路径经过相同数量的 0 和 1](https://leetcode.cn/problems/check-if-there-is-a-path-with-equal-number-of-0s-and-1s/)（会员题） `同2267`

## 网格图优化DP

- [1289. 下降路径最小和 II](https://leetcode.cn/problems/minimum-falling-path-sum-ii/)(记录最小下标)

- [1937. 扣分后的最大得分](https://leetcode.cn/problems/maximum-number-of-points-with-cost/) (拆项)&#x1F60D;&#x1F60D; `挺好的题`
