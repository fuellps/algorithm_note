### 模板

最经典的单调栈是完成下面的两个操作:

- 求数组中每个元素右边严格小于(大于)自己的元素位置
- 求数组中每个元素左边严格小于(大于)自己元素的位置

> 对于严格小于,可以维护单调递增的单调栈(底小顶大)
>
> 对于严格大于,可以维护单调递减的单调栈(底大顶小)

$注意:对于栈顶元素与入栈元素相同时是保留/弹出需要依据题目具体分析.$

>  模板题:[单调栈结构(进阶)](https://www.nowcoder.com/practice/2a2c00e7a88a498693568cef63a4b7bb) : 
>
> 求数组中每个元素左边和右边严格小于自己的元素位置,不存在输出-1.

```c++
#include<bits/stdc++.h>
using namespace std;
int main() {
    ios::sync_with_stdio(false);cin.tie(0);
    int n;cin >> n;
    vector<int> nums(n);
    for (int i = 0; i < n; ++i) {
        cin >> nums[i];
    }
    vector<int> left(n, -1),right(n, -1);
    stack<int> st;
    for (int i = 0; i < n; ++i) {
        int x = nums[i];
        // 模板开始
        while (!st.empty() && nums[st.top()] >= x) {
            int j = st.top();
            st.pop();
            right[j] = i;
            if(! st.empty()) left[j] = st.top();
        }
        st.push(i);
        //模板结束
    }
   // 结算阶段 
    while (!st.empty()) {
        int j = st.top();
        st.pop();
        if (!st.empty()) {
            left[j] = st.top();
        }
    }
//修正阶段:因为数组中可能有重复元素,那么右边第一个小于自身的元素位置可能是与自身相等(因此栈顶与入栈元素相同也弹出).那么只需从后往前遍历,如果发现是一样的,就修改为后面已经修正对的位置.
    for (int i = n - 1; i >= 0; --i) {
        if (right[i] != -1 && nums[i] == nums[right[i]]) {
            right[i] = right[right[i]];
        }
    }

    for (int i = 0; i < n; ++i) {
        cout << left[i] << " " << right[i] << "\n";
    }

    return 0;
}
```

### trick

> 对于某些需要结算阶段的题目,可以加入哨兵节点,简化代码逻辑.但是必须保证原数组中所有元素都能被弹出,且加入的哨兵节点不会影响答案.

以[1504. 统计全 1 子矩形](https://leetcode.cn/problems/count-submatrices-with-all-ones/)为例.

```python
class Solution:
    def numSubmat(self, mat: List[List[int]]) -> int:
        n,m = len(mat),len(mat[0])
        heights = [0]*(m+1)
        heights[-1] = -1 #添加哨兵.在后面计算不会影响到答案.
        ans = 0
        for i,row in enumerate(mat):
            for j,x in enumerate(row):
                heights[j] = 0 if x == 0 else heights[j] + 1
            ans += self.countingRectangle(heights)
        return ans

    def countingRectangle(self,heights):
        ans = 0
        st = []
        #对于当前的柱状图,计算小于heights[i]的左边界heights[l],有边界heights[r]
        #所能形成的矩阵个数为 (heights[i]-max(heights[l],heights[r]))*(r-l-1)*(r-l)//2
        for i,x in enumerate(heights):
            while st and heights[st[-1]] >= x:
                cur = st.pop()
                left = st[-1] if st else -1
                # 相等时计算也不会影响答案,因为 (heights[i]-max(heights[l],heights[r])) = 0
                ans += (heights[cur] - max(0 if left == -1 else heights[left],heights[i]))*(i-left-1)*(i-left)//2
            st.append(i)
        return ans               


```



### 题目练习

#### 基础

- [739. 每日温度](https://leetcode.cn/problems/daily-temperatures/)
- [单调栈结构(进阶)](https://www.nowcoder.com/practice/2a2c00e7a88a498693568cef63a4b7bb) 牛客

#### 维护答案的可能性

- [962. 最大宽度坡](https://leetcode.cn/problems/maximum-width-ramp/) 1608
- [大鱼吃小鱼](https://www.nowcoder.com/practice/77199defc4b74b24b8ebf6244e1793de)
- [四元组问题](https://www.lanqiao.cn/courses/21968/learning/?id=1622975&compatibility=false) `判断是否满足 a<b<c<d,且nums[d] < nums[c] < nums[a] < nums[b]`  &#x1F60D;

#### 矩阵

- [84. 柱状图中最大的矩形](https://leetcode.cn/problems/largest-rectangle-in-histogram/) 经典题
- [85. 最大矩形](https://leetcode.cn/problems/maximal-rectangle/)
- [1504. 统计全 1 子矩形](https://leetcode.cn/problems/count-submatrices-with-all-ones/)

#### 贡献法

- [907. 子数组的最小值之和](https://leetcode.cn/problems/sum-of-subarray-minimums/) 1976 经典题

#### 最小字典序

-  [402. 移掉 K 位数字](https://leetcode.cn/problems/remove-k-digits/) ~1800
-  https://www.luogu.com.cn/problem/P1106 同402
-  [1673. 找出最具竞争力的子序列](https://leetcode.cn/problems/find-the-most-competitive-subsequence/) 1802
-  [316. 去除重复字母](https://leetcode.cn/problems/remove-duplicate-letters/) 2185

>  [天池-03. 整理书架](https://leetcode.cn/contest/tianchi2022/problems/ev2bru/) 同316 扩展：重复个数不超过limit个

-  [321. 拼接最大数](https://leetcode.cn/problems/create-maximum-number/) 分治，如何归并使得字典序最大?
-  [2030. 含特定字母的最小子序列](https://leetcode.cn/problems/smallest-k-length-subsequence-with-occurrences-of-a-letter/) 2562 `限制较多，必须包含letter字符至少repeatition个`
