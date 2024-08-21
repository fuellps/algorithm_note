trie树适用于高效查找和存储某个字符串.

trie树的大小需要开到与总字符串长度相同的长度.每个节点存储字符串的种类.例如对于小字母而言,trie树应该开到trie[N]\[26].同时一般以0号节点表示空节点.一般还需要1个cnt数组表示以哪个前缀结束的字符串个数.

代码示例如下:

```java
static int N = 100010;
static int[][] trie = new int[N][26];
//核心代码1:向前缀树插入1个字符串
void insert(char[] s){
    int p = 0;//头节点.
    for(int i = 0; i < s.length; i++){
        int pos = s[i] - 'a';//对应在节点的哪个子结点上.
        if(!trie[p][pos]){//不存在该节点(字符).
            trie[p][pos] = ++idx;//新建一个节点
        }
        p = trie[p][pos];//跳到该字符对应得节点
    }
    cnt[p]++;//加入1个前缀.
}

//核心代码2:查询某个字符串出现多少次
int query(char[] s){
    int p = 0;
    for(int i = 0;i < s.length; i++){
        int pos = s[i] - 'a';
        if(!trie[p][pos]) return 0;//不存在该字符节点.
        p = trie[p][pos];
    }
    return cnt[p];
}
```

最大异或对

暴力做法:

```java
for(int i = 0; i < n ; i++){
    for(int j = 0; j < i; j++){
		 ans = max(ans,a[i]^ a[j]);//a[j]^a[i]结果也是一样的,所以可以人为规定顺序.
   }
}
```

a[i]^a[j]可以用trie树进行优化.每次比较31位二进制数即可.

```c++
void insert(int a){
    int p = 0;
    for(int i = 30; i >= 0; i--){
        int pos = a>>i&1;
        if(!trie[p][pos]) trie[p][pos] = ++idx;
        p = trie[p][pos]; 
    }
}
int query(int a){
    int res = 0,p = 0;
    for(int i = 30; i >= 0; i--){
        int pos = a>>i&1;
        if(trie[p][!pos]){//存在高位不同的数.
            res |= 1<<i;
            p = trie[p][!pos];//继续看下一位是否还能不同
        }
        else {
            p = trie[p][pos];//不得
        }
    }
    return res;
}
```

