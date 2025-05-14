### 模板题

- https://www.luogu.com.cn/problem/P2036 `子集（幂集）型枚举模板题`
- https://www.luogu.com.cn/problem/P1157 `求组合模板题`
- https://www.luogu.com.cn/problem/P1706 `全排列模板题`
- 

### 简单枚举练手题

- [既约分数](https://www.lanqiao.cn/problems/593/learning/?page=1&first_category_id=1&name=%E6%97%A2%E7%BA%A6%E5%88%86%E6%95%B0) 

### 暴力枚举/搜索

- https://www.luogu.com.cn/problem/P2241`给定方格大小，判断有多少个正方形和长方形` 

- [顺子日期](https://www.lanqiao.cn/problems/2096/learning/?page=1&first_category_id=1&name=%E9%A1%BA%E5%AD%90%E6%97%A5%E6%9C%9F) `判断某一年是否均有顺子`

- [小明和完美序列](https://www.lanqiao.cn/problems/3199/learning/?page=1&first_category_id=1&name=%E5%B0%8F%E6%98%8E%E5%92%8C%E5%AE%8C) `每次将长度为k的区间涂成同一颜色,求最少涂的次数。`

- https://www.luogu.com.cn/problem/P2089 `爆搜`

- [选题](https://www.lanqiao.cn/problems/3263/learning/?page=1&first_category_id=1&name=%E9%80%89%E9%A2%98) `爆搜` 

- https://www.luogu.com.cn/problem/P1618 `全排列爆搜`

- [串变换](https://www.lanqiao.cn/problems/4360/learning/?page=1&first_category_id=1&name=%E4%B8%B2%E5%8F%98%E6%8D%A2)`带不选的全排列爆搜`

- https://www.luogu.com.cn/problem/P1088 `给定排列之后的第m个排列` `挺好的全排列练习题`

- https://www.luogu.com.cn/problem/P3392  `暴力枚举`

  > 求 从最上方若干行（至少一行）的格子全部是白色的；接下来若干行（至少一行）的格子全部是蓝色的；剩下的行（至少一行）全部是红色的；的最小操作次数。			

- https://www.luogu.com.cn/problem/P3654  `注意有坑点; `    `做到O(n^2)`

  > 给定n*m矩阵，其中有一些障碍物。给定1 <= k <= min(n,m),求 $1\times k$大小的块的数量。

- https://www.luogu.com.cn/problem/P1217 `输出[a,b]中的回文质数`

> 有个小结论:偶数回文串除了11之外都不是质数。
>
> 因为：11的整除判定方法：奇数位之和减去偶数位之和能被11整除。(从右往左编号。)

- https://www.luogu.com.cn/problem/P1149 `根据火柴计算A+B=C的方案数`
- https://www.luogu.com.cn/problem/P3799 `给定n个木棒，求选出4个木棒组成正方形的方案数.`
- [笨笨的机器人](https://www.lanqiao.cn/problems/3262/learning/?page=1&first_category_id=1&name=%E7%AC%A8%E7%AC%A8%E7%9A%84%E6%9C%BA%E5%99%A8%E4%BA%BA) `机器人只要走7步就回到原点.求机器人回到原点的概率.` `注意精度问题.`
- [取数游戏](https://www.luogu.com.cn/problem/P1123)
- 

###### 分解子问题

- https://www.luogu.com.cn/problem/P3612 `给定s.每次将s右移一位拼接在原字符串。求第K个字符`
- https://www.luogu.com.cn/problem/P1259 `给定黑白棋子。输出使其黑白相间的路径。`
- https://www.luogu.com.cn/problem/P1010 `给定一个数。要求表示为2的幂方形式。如5:2(2) + 2(0),7:2(2)+2+2(0)`
- https://www.luogu.com.cn/problem/P1228 `给定2^k * 2^k的矩形，同时给定4个L型块，要求填充矩阵只剩1个位置。`

###### 字符串与搜索

- https://www.luogu.com.cn/problem/P1032 	`字符串库函数练习题；注意有坑点`
- https://www.luogu.com.cn/problem/P1019 `单词接龙，一个词前缀与龙后缀相同，但不能包含龙`
- [212. Word Search II](https://leetcode.cn/problems/word-search-ii/) `单词搜索。字典树优化剪枝。`



###### 嵌套表达式搜索

- [772. Basic Calculator III](https://leetcode.cn/problems/basic-calculator-iii/) `实现带（）的表达式，题目保证式子合法且不含空格。`
- [394. Decode String](https://leetcode.cn/problems/decode-string/)  `d[XXX]形式`
- https://www.luogu.com.cn/problem/P1928 `[dXXX]形式`
- https://leetcode.cn/problems/number-of-atoms/description/ `xxd形式`



#### 优化的枚举

- [最大通过数](https://www.lanqiao.cn/problems/3346/learning/?page=1&first_category_id=1&name=%E6%9C%80%E5%A4%A7%E9%80%9A%E8%BF%87%E6%95%B0) `给定数组a,b,求两个数组前缀和<=k的最大长度之和。`
- [P2105 K皇后](https://www.luogu.com.cn/problem/P2105) `很好的习题`
- [大石头的搬运工](https://www.lanqiao.cn/problems/3829/learning/?page=1&first_category_id=1&name=%E5%A4%A7%E7%9F%B3%E5%A4%B4%E7%9A%84) `n堆石头，有重量和位置。移动n-1轮，求最小移动代价。`  `前后缀分解 or 拆项 ` &#x1F60D;
- [最大子数组](https://www.lanqiao.cn/problems/3260/learning/?page=1&first_category_id=1&name=%E6%9C%80%E5%A4%A7%E6%95%B0%E7%BB%84) `不能贪心,每次删除最大1个数或者山吹最小的两个数，执行k次，求数组最大和。`  &#x1F60D;
- [四元组问题](https://www.lanqiao.cn/courses/21968/learning/?id=1622975&compatibility=false) `判断是否满足 a<b<c<d,且nums[d] < nums[c] < nums[a] < nums[b]`  `课程`&#x1F60D;





#### 树/图上的搜索

- [黄金树](https://www.lanqiao.cn/problems/4494/learning/?page=1&first_category_id=1&name=%E9%BB%84%E9%87%91%E6%A0%91) `二叉树的自顶向下DFS`
- [仙境诅咒](https://www.lanqiao.cn/problems/3935/learning/?page=1&first_category_id=1&name=%E4%BB%99%E5%A2%83%E8%AF%85%E5%92%92) `抽象成图问题`
- [混沌之地](https://www.lanqiao.cn/problems/3817/learning/?page=1&first_category_id=1&name=%E6%B7%B7%E5%A2%83%E4%B9%8B%E5%9C%B0) `网格图判断路径是否存在.多了一个条件,可以破坏一个障碍物.`
- [混沌之地5](https://www.lanqiao.cn/problems/3820/learning/?page=1&first_category_id=1&name=%E6%B7%B7%E5%A2%83%E4%B9%8B%E5%9C%B0) `同上一题,修改了相应条件.`
- [01迷宫](https://www.luogu.com.cn/problem/P1141) `网格图搜索`
- 





## TODO:下面习题待整理

##### 记忆化搜索(大部分习题可在动态规划中练习，这里只是引入思想)

- https://www.luogu.com.cn/problem/P1464 `模板题`




#### 宽度优先搜索

- [穿越雷区](https://www.lanqiao.cn/problems/141/learning/?page=1&first_category_id=1&problem_id=131) 基础
- [青蛙跳杯子](https://www.lanqiao.cn/problems/102/learning/?page=1&first_category_id=1&problem_id=102)
- [Luogu P1225 黑白棋游戏](https://www.luogu.com.cn/problem/P1225)
- [长草](https://www.lanqiao.cn/problems/149/learning/?page=1&first_category_id=1&problem_id=131)
- [迷宫与陷阱](https://www.lanqiao.cn/problems/229/learning/?page=1&first_category_id=1&problem_id=223) 变形题 &#x1F60D; &#x1F60D;
- [调手表](https://www.lanqiao.cn/problems/230/learning/?page=1&first_category_id=1&problem_id=223)
- [九宫重排](https://www.lanqiao.cn/problems/261/learning/?page=1&first_category_id=1&problem_id=223)
- [490. 迷宫](https://leetcode.cn/problems/the-maze/) 会员题
- https://www.luogu.com.cn/problem/P1825 `变形题，有传送梯如何做？`



### 暴力枚举

https://codeforces.com/problemset/problem/681/B 1300
- [2207. 字符串中最多数目的子序列](https://leetcode.cn/problems/maximize-number-of-subsequences-in-a-string/) 1550

### 枚举右维护左

- [1. 两数之和](https://leetcode.cn/problems/two-sum/)
  
  - https://codeforces.com/problemset/problem/702/B
- [1512. 好数对的数目](https://leetcode.cn/problems/number-of-good-pairs/) 1161 经典题
  
    - https://leetcode.cn/problems/sum-of-digit-differences-of-all-pairs/
    - 反向构造 https://codeforces.com/problemset/problem/1927/B 900
      https://leetcode.com/discuss/interview-question/3685049/25-variations-of-Two-sum-question
      https://codeforces.com/problemset/problem/1420/B 1200
      https://codeforces.com/problemset/problem/318/B 1300 子串
    
 - [“非常男女”计划](https://www.luogu.com.cn/problem/P1114)
 - 
  #### 枚举右，维护左：需要维护两种值（pair）&#x1F60D;

  https://codeforces.com/problemset/problem/1931/D 1300  同余原理&#x1F60D;
  https://leetcode.cn/problems/count-beautiful-substrings-ii/ 2445

- [Counting Pairs](https://codeforces.com/problemset/problem/2051/D) `经典的题改造`

哈希表
- [2260. 必须拿起的最小连续卡牌数](https://leetcode.cn/problems/minimum-consecutive-cards-to-pick-up/) 1365
- [982. 按位与为零的三元组](https://leetcode.cn/problems/triples-with-bitwise-and-equal-to-zero/) 2085
- [面试题 16.21. 交换和](https://leetcode.cn/problems/sum-swap-lcci/)

- [421. Maximum XOR of Two Numbers in an Array](https://leetcode.cn/problems/maximum-xor-of-two-numbers-in-an-array/) `数组中两数的最大异或和。哈希做法很有趣。`

前缀和
https://codeforces.com/problemset/problem/466/C

前缀和+哈希表（双变量思想）
- [560. 和为 K 的子数组](https://leetcode.cn/problems/subarray-sum-equals-k/)
   - 子数组中的和为 k 的子数组的个数之和 https://codeforces.com/problemset/problem/1996/E 1600
   
- [974. 和可被 K 整除的子数组](https://leetcode.cn/problems/subarray-sums-divisible-by-k/) 1676
   - 变形：乘积可以被 k 整除
   
     

### 余数

- [2050C - Uninteresting Number](https://codeforces.com/problemset/problem/2050/C) `很好的习题`
