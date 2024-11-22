## 套路



$$
一般定义dp[i][j]表示前i个数中,在什么要求下,第i个数处于第j状态时的最优值\\
对于位置i,考虑每个状态如何转移而来
$$

对于状态机DP,大多数题目的某些状态是不合法的,不论如何,需要保证状态的合法性.



### 习题练习:



#### 必须/最多执行1次相关

$一般定义dp[i][j]表示在前i个元素中..要求下,位置i是否执行操作的最优值$

[1493. 删掉一个元素以后全为 1 的最长子数组](https://leetcode.cn/problems/longest-subarray-of-1s-after-deleting-one-element/)

[1186. 删除一次得到子数组最大和](https://leetcode.cn/problems/maximum-subarray-sum-with-one-deletion/)

[1746. 经过一次操作后的最大子数组和](https://leetcode.cn/problems/maximum-subarray-sum-after-one-operation/)(会员题)

#### 被k整除相关

$一般定义dp[i][j]表示前i个元素中..要求下,模k的余数为j的最优值$

[1262. 可被三整除的最大和](https://leetcode.cn/problems/greatest-sum-divisible-by-three/)

[1363. 形成三的最大倍数](https://leetcode.cn/problems/largest-multiple-of-three/)(构造答案)



#### 乘积相关

$对于乘积类型,一般需要知道前i个数中的最小值和最大值相关的性质$

[1567. 乘积为正数的最长子数组长度](https://leetcode.cn/problems/maximum-length-of-subarray-with-positive-product/)

[2708. 一个小组的最大实力值](https://leetcode.cn/problems/maximum-strength-of-a-group/)

[1594. 矩阵的最大非负积](https://leetcode.cn/problems/maximum-non-negative-product-in-a-matrix/)



#### 形成特殊字符串类型相关

$这类题目要求的特定字符串一般很小,一般定义dp[i][0]表示全为第1个字符的相关状态,\\dp[i][1]表示为第1个字符和第2个字符的相关状态,\\...一次类推$

[1955. 统计特殊子序列的数目](https://leetcode.cn/problems/count-number-of-special-subsequences/)

[LCP 19. 秋叶收藏集](https://leetcode.cn/problems/UlBDOe/)



#### 交替和相关



#### 其他类型

##### 股票系列

$一般定义dp[i][j]表示在前i场交易中,位置i是否持有股票的最优值.如果有个数限制,则添加约束即可$

[121. 买卖股票的最佳时机](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock/)

[122. 买卖股票的最佳时机 II](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-ii/)

[123. 买卖股票的最佳时机 III](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-iii/)

[188. 买卖股票的最佳时机 IV](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-iv/)

[309. 买卖股票的最佳时机含冷冻期](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-with-cooldown/)

[714. 买卖股票的最佳时机含手续费](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/)

##### 其他

[3259. 超级饮料的最大强化能量](https://leetcode.cn/problems/maximum-energy-boost-from-two-drinks/)

[2361. 乘坐火车路线的最少费用](https://leetcode.cn/problems/minimum-costs-using-the-train-line/)(会员题)

[2222. 选择建筑的方案数](https://leetcode.cn/problems/number-of-ways-to-select-buildings/)(长度限制,不能相邻)

[376. 摆动序列](https://leetcode.cn/problems/wiggle-subsequence/)(正负)

[2786. 访问数组中的位置使分数最大](https://leetcode.cn/problems/visit-array-positions-to-maximize-score/)(奇偶性)

[1911. 最大子序列交替和](https://leetcode.cn/problems/maximum-alternating-subsequence-sum/)(奇偶性)

[2036. 最大交替子数组和](https://leetcode.cn/problems/maximum-alternating-subarray-sum/)(会员题)

[3196. 最大化子数组的总成本](https://leetcode.cn/problems/maximize-total-cost-of-alternating-subarrays/)

[3290. 最高乘法得分](https://leetcode.cn/problems/maximum-multiplication-score/)

[2745. 构造最长的新字符串](https://leetcode.cn/problems/construct-the-longest-new-string/)

[1537. 最大得分](https://leetcode.cn/problems/get-the-maximum-score/):red_circle:

[276. 栅栏涂色](https://leetcode.cn/problems/paint-fence/) :red_circle:(会员题)

[1395. 统计作战单位数](https://leetcode.cn/problems/count-number-of-teams/)

[2826. 将三个组排序](https://leetcode.cn/problems/sorting-three-groups/)

[2771. 构造最长非递减子数组](https://leetcode.cn/problems/longest-non-decreasing-subarray-from-two-arrays/)

[801. 使序列递增的最小交换次数](https://leetcode.cn/problems/minimum-swaps-to-make-sequences-increasing/) :red_circle:



比较难想的状态:

[2919. 使数组变美的最小增量运算数](https://leetcode.cn/problems/minimum-increment-operations-to-make-array-beautiful/)(距离限制)