对于求[1~n]中的字典序第k小的数,可以通过从高位开始构造,计算出每个前缀所包含的值.

> 如果前缀个数小于等于n,说明当前前缀在n的左边.扩大当前的前缀.
>
> 否则,说明字典序第k小的数的当前的前缀已经确定,扩大一位去寻找下一位.



```java
 //注意:用int做参数时可能会溢出.建议用long
long cal(long n,long lo,long hi){
    long res = 0;
    while(lo <= n){
        res += min(n + 1, hi) - lo;
        lo *= 10;
        hi *= 10;
    }
}

long findKthNumber(long n,long k){
    int cur = 1;
    while(k > 1){
		long step = cal(n,cur, cur + 1); //计算以cur为前缀中,<=n的数字个数
        if(step < k){//小于k个数
            k -= step;
            cur++; //扩大前缀
        }else{ //大于等于k个数
            cur *= 10;
            k--;
        }
    }
    return 
}
```

