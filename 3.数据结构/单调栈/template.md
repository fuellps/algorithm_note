单调栈可以用于求每个元素两边严格大于/小于它的元素位置(不存在为-1)

> [P5788 【模板】单调栈](https://www.luogu.com.cn/problem/P5788) 
>
> 题意:求数组中每个元素严格大于它的元素位置,不存在输出0.

```c++
#include <bits/stdc++.h>
using namespace std;
const int N = 3e6 + 10;
int a[N],ans[N],n;
int main(){
    stack<int> st;
    cin >> n;
    // 从左往右遍历的做法:维护单调递减的栈.
    //栈中保留的元素即为不存在更大元素的位置
    for(int i = 0;i < n; i++){
        cin >> a[i];
        while(!st.empty() && a[i] > a[st.top()]){
            int idx =  st.top();
            ans[idx] = idx;
            st.pop();
        }
    }
    for(int i = 0;i < n; i++){
        if(ans[i]) cout << ans[i] + 1 << " ";
        else cout << 0 << " ";
    }
}
```

