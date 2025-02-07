## 模板

这类题一般都是统计一段区间内数字的相关性质

```java
统计[1~N]范围内数字相关的性质
    dfs(i)表示从高位开始构造,当前位置所能构造的合法数字
    int dfs(int i,boolean limit,boolean isNum){
    if(i == len(N)) return isNum ? 1 : 0 ; //到达这时说明找到一个数字
    //在没有约束的情况下,已经计算过了
    if(!limit && isNum && dp[i] != -1) return dp[i];
    int res = 0;
    //前面没有填数字,后面也可以不填数字
    if(!isNum) res = dfs(i + 1,false,false);
    int up = limit ? high[i] - '0' : 9;
    //已经处理过前导0了,如果前面是数字就可以从0开始,不是数字就只能从1开始
    for(int d = isNum ? 0 : 1; d <= up; d++){
        res += dfs(i + 1, limit && d == up, true);
    }
    //没有约束的情况下,记录答案
    if(isNum && !limit) return dp[i] = res;
    return res;
}
```

```java
统计[L~R]范围内数字相关的性质,其中L,R均为正数( > 0 )
    dfs(i)表示从高位开始构造,当前位置所能构造的合法数字
    int dfs(int i,boolean l_low,boolean l_high,boolean isNum){
    if(i == len(N)) return isNum ? 1 : 0 ; //到达这时说明找到一个数字
    //在没有约束的情况下,已经计算过了
    if(!l_low && l_high && isNum && dp[i] != -1) return dp[i];
    int res = 0;
    //低位为0说明是之前补前导0,可以填0
    if(low[i] == '0' && !isNum) res = dfs(i + 1,true,false,false);
    int hi = l_high ? high[i] - '0' : 9;
    int lo = l_low ? low[i] - '0' : 0;
    int d0 = isNum ? 0 : 1;
    //当前位必须同时满足大于lo和d0,
    for(int d = Math.max(d0,lo); d <= up; d++){
        res += dfs(i + 1,l_low && d == lo, l_high && d == hi, true);
    }
    //没有约束的情况下,记录答案
    if(isNum && !l_high && !l_low) return dp[i] = res;
    return res;
}
```



习题练习:

1.https://vjudge.net/problem/CodeForces-855E#author=GPT_viSalazar Slytherin's Locket

 注意:对于这道题,记忆化数组得逆序存放.因为dfs是从低位开始构造,而对应的下标是从高位开始.
