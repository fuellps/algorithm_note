### 最长递增子序列(LIS)

$$
\begin{aligned}
&最长递增子序列是有\textbf{数值元素相邻位置依赖}的,所以一般用枚举选哪个的思路 \\
&做法1:定义dp[i]表示以i结尾的最长递增子序列 \\
&考虑以i结尾的最长递增子序列从哪里转移而来 \\
&枚举 j<i,如果a[j] < a[i],那么dp[i]可从dp[j] + 1转移而来。
\end{aligned}
$$



```java
int ans = 0; //记录数组中的最长递增子序列
int[] dp = new int[n];
for(int i = 0;i < n; i++){
    dp[i] = 1; //以i结尾的最长递增子序列的长度至少为1
    for(int j = 0;j < i ; j++){
        if(nums[j] < nums[i]){
            dp[i] = Math.max(dp[i], dp[j] + 1);
        }
    }
    ans = Math.max(ans,dp[i]);
}
return ans;
```


$$
\begin{aligned}
&做法2:定义f[i]表示长度为i+1的递增子序列的末尾元素的最小值 \\
&贪心的想,要使最长递增子序列越长,则最长递增子序列前一个元素(末尾元素)尽可能越小越好 \\
&因此每次查找一个数,就在f数组中找到第一个大于等于他的数,如果找到就替换, \\
&找不到说明当前数能组成更大长度的最长递增子序列.
\end{aligned}
$$




```java
 // List<Integer> f = new ArrayList<>(); 列表
int[] f = new int[n]; //也可以用数组维护,最长递增子序列长度不会超过n
int len = 0;//最长递增子序列长度
for(int x : nums){
    int j = lower_bound(f,len,x);
    if(j == len){
        f[len++] = x;//能组成更长的递增子序列
    }else{
        f[j] = x;//在当前最长递增子序列末尾元素及前面替换成更小的数
    }
}

```

#### 习题练习

##### 基础

-  [300. 最长递增子序列](https://leetcode.cn/problems/longest-increasing-subsequence/)
-  [2826. 将三个组排序](https://leetcode.cn/problems/sorting-three-groups/) 1721
-  [1671. 得到山形数组的最少删除次数](https://leetcode.cn/problems/minimum-number-of-removals-to-make-mountain-array/) 1913
-  [1964. 找出到每个位置为止最长的有效障碍赛跑路线](https://leetcode.cn/problems/find-the-longest-valid-obstacle-course-at-each-position/) 1933
-  [2111. 使数组 K 递增的最少操作次数](https://leetcode.cn/problems/minimum-operations-to-make-the-array-k-increasing/) 1941

##### 进阶

-  [1626. 无矛盾的最佳球队](https://leetcode.cn/problems/best-team-with-no-conflicts/) 2027 `可用树状数组优化`
-  [673. 最长递增子序列的个数 ](https://leetcode.cn/problems/number-of-longest-increasing-subsequence/)`可用树状数组优化`
-  [354. 俄罗斯套娃信封问题](https://leetcode.cn/problems/russian-doll-envelopes/) 二维 LIS
- [1691. 堆叠长方体的最大高度](https://leetcode.cn/problems/maximum-height-by-stacking-cuboids/) 2172
-  [2407. 最长递增子序列 II](https://leetcode.cn/problems/longest-increasing-subsequence-ii/) 2280 线段树优化DP



### 最长公共子序列(LCS)

这类题目一般是与**子序列匹配有关的问题**
$$
\begin{aligned}
&前言:对于两个字符串的子序列\textbf{匹配}问题,\\
&一般定义dfs(i,j)表示s中下标从0到i,与t中下标从0到j的..处理结果\\
&一般根据题意,考虑第i个字符与第j的字符是否匹配,做相应处理.\\
&递归边界:i < 0 或 j < 0,表示其中某个字符串为空,根据题意做相关处理
\end{aligned}
$$

#### 示例/模板

>  给你两个字符串s,t,求s和t的最长公共子序列长度

$$
\begin{aligned}
&定义dp[i][j]表示s中前i个字符与t中前j个字符的最长公共子序列长度\\
&考虑s中第i个字符和第j个字符选或不选:\\
&贪心的想,如果s[i]=t[j],那么肯定选当前字符的子序列长度最好.因此从dfs(i-1,j-1)+1转移 \\
&如果s[i]!=s[j],那么就只不选1个字符,从max(dfs(i-1,j),dfs(i,j-1))转移而来\\
&边界条件:i <0 || j < 0,表示其中1个字符串为空,则最长公共子序列长度为0
\end{aligned}
$$



```java
//经典模板：
int[][] dp = new int[n+1][m+1];//个插入1个状态,规避边界讨论
//初始化:全为0,因此默认值就是初始化值
for(int i = 0; i < n; i++){
    for(int j = 0;j < m; j++){
        if(s[i] == t[j]){
            dp[i+1][j+1] = dp[i][j] + 1;
        }else{
            dp[i+1][j+1] = max(dp[i+1][j], dp[i][j+1]);
        }
    }
}


//空间优化:每个状态依赖于上面的格子,左上角的格子,左边已经计算好的格子->(内层循环需正序遍历)
int[] dp = new int[m + 1];//默认值就是边界值
for(int i = 0;i < n; i++){
    int prev = dp[0];
    //有些题目需要在这里更新dp[0]的值
    dp[0] = 0; //对于这道题可不写 
    for(int j = 0; j < m; j++){
        int tmp = dp[j+1]; //保存下一个左上角的值
        if(s[i] == t[j]){
            dp[j+1] = prev + 1;
        }else{
            dp[j+1] = max(dp[j],do[j+1]);
        }
        
    }
}

```

>  求个数版本



```c++
#include<bits/stdc++.h>

using namespace std;
using ll = long long;

//空间优化版本
void solve() {
	string s,t;cin >> s >> t;
	n = s.size(),m = t.size();
    //f表示最长公共子序列的个数，g表示最长公共子序列的长度
	fill(f,f+m+1,1);
	for(int i =0 ;i < n; i++){
		int pf = f[0],pg = g[0];//记录左上角
		for(int j = 0;j < m ;j++){
			int tf = f[j+1],tg = g[j+1];//记录上面格子
			f[j+1] = g[j+1] = 0;//清除遗留的状态
			if(s[i] == t[j]){
				g[j+1] = pg + 1;
				f[j+1] = pf;
			}else{
				g[j+1] = max(g[j],tg);
			}
			if(g[j+1] == g[j]) f[j+1] += f[j];//可以从左边格子转移而来
			if(g[j+1] == tg) f[j+1] += tf;//可以从上边格子转移而来
			if(g[j+1] == pg) f[j+1] -= pf;//上边格子和左边格子都经过左上角格子，去除重复
			pf = tf,pg = tg; //更新下一轮的左上角
		}
	}
	cout << g[m] << endl << f[m] << endl;
}
```



#### 习题练习

##### 1.0两个子序列互斥

- [1143. 最长公共子序列](https://leetcode.cn/problems/longest-common-subsequence/)

> 进阶：[P2516 最长公共子序列](https://leetcode.cn/link/?target=https%3A%2F%2Fwww.luogu.com.cn%2Fproblem%2FP2516) 求最长公共子序列的个数
>
> [P1439 【模板】最长公共子序列](https://www.luogu.com.cn/problem/P1439) 用LIS求LCS，很有趣
>
> 上题的简化版本：[115. 不同的子序列](https://leetcode.cn/problems/distinct-subsequences/) 
>
> 扩展题：[U396793 最长公共子串](https://www.luogu.com.cn/problem/U396793) `求两个字符串的最长公共子串`

- [1035. 不相交的线](https://leetcode.cn/problems/uncrossed-lines/)

- [583. 两个字符串的删除操作](https://leetcode.cn/problems/delete-operation-for-two-strings/)

- [712. 两个字符串的最小ASCII删除和](https://leetcode.cn/problems/minimum-ascii-delete-sum-for-two-strings/)

- [1458. 两个子序列的最大点积](https://leetcode.cn/problems/max-dot-product-of-two-subsequences/)**(要求子序列非空做法)**
-  [3290. 最高乘法得分](https://leetcode.cn/problems/maximum-multiplication-score/) 1692  `类似1458，边界更难`

##### 2.0将一个/两个字符串变成另1个字符串.

- [72. 编辑距离](https://leetcode.cn/problems/edit-distance/)

- [97. 交错字符串](https://leetcode.cn/problems/interleaving-string/)

- [44. 通配符匹配](https://leetcode.cn/problems/wildcard-matching/)

- [10. 正则表达式匹配](https://leetcode.cn/problems/regular-expression-matching/)

##### 3.0要求一个字符串是另一个字符串的子序列(状态转移方程类型01背包)

> 根据状态压缩的不同对象，恰好就是完全背包或者01背包。

- [115. 不同的子序列](https://leetcode.cn/problems/distinct-subsequences/)

- [1092. 最短公共超序列](https://leetcode.cn/problems/shortest-common-supersequence/)(构造答案)

-  [3316. 从原字符串里进行删除操作的最多次数](https://leetcode.cn/problems/find-maximum-removals-from-source-string/) 2062 (求最值做法)

- [1639. 通过给定词典构造目标字符串的方案数](https://leetcode.cn/problems/number-of-ways-to-form-a-target-string-given-a-dictionary/) (求方案数做法) `类似115`
- 