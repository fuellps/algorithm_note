## 常用内容及语法

### 快读类

```java
class FastReader{
    BufferedReader br;
    StringTokenier st;
    public FastReader(){
        br = new BufferedReader(new InputStreamReader(System.in));
    }
    String next(){
       try{
            while(st == null || !st.hasMoreElements()){
            st = new StringTokenizer(br.readLine());
        }
        return st.nextToken();
       }catch(Exception e){
           
       }
        return null;
    }
    
    int nextInt(){
        return Integer.parseInt(next());
    }
    long nextLong(){
        return Long.parseLong(next());
    }
    
    double nextDouble(){
        return Double.parseDouble(next());
    }
}
```

### 快写

```java
PrintWriter out = new PrintWriter(System.out);


out.close(); //注意，最后要关闭输出流才能输出到终端.
```

### Lambda表达式

1. ()内参数类型可省略
2. 如果只有一个参数，可省略()
3. 只有一条语句，可省略return语句，{}

```java
//类如下：
class Stu{
    String name;
    int score;
    public Stu(String name, int score) {
        this.name = name;
        this.score = score;
    }
    public Stu(){}
    @Override
    public String toString(){
        return name + " " + score;
    }
}
static void solve() {
        Stu[] stus = new Stu[3];
        stus[0] = new Stu("ab",87);
        stus[1] = new Stu("a",87);
        stus[2] = new Stu("c",100);
    //只有一条语句，省略return 和 {}
        Arrays.sort(stus,(a,b) ->  a.score == b.score ? b.score-a.score : a.name.compareTo(b.name));
        for(Stu s : stus) {
            out.println(s);
        }
  -----------------------------------------------------------
    int[] nums = {1,30,4382,32891,340,4320};
        PriorityQueue<Integer> pq = new PriorityQueue<>((a,b)->b-a); //大根堆
        List[] g = new List[N];
        //1个参数，圆括号可省略
        Arrays.setAll(g, i -> new ArrayList<>()); 
    }



```



## API

### ArrayList

```java
List<Integer> a = new ArrayList<>(); //初始化空列表
List<Integer> a = new ArrayList<>(30); //初始化长度为30,注意是容量，列表大小仍然为0
List<Integer> a = new ArrayList<>(b); //y
```



### Character类

$isLetterOrDigit(char \ c)$ 判断字符是否为数字或字母



*****

### String类

两个字符串比较函数: $s.compareTo(t)$ 如果s的字典序比t小,返回负数.如果s的字典序比t大,返回正数.相等时返回0



*****

### TreeSet类

TreeSet类是基于红黑树实现的.

基本方法和Set一致

有几个比较好用的API:

$first()$ 获取有序表中的第一个元素

$last()$ 获取有序表中的最后一个元素

$ceiling(E\ e)$获取大于等于e的第一个元素, **找不到返回null**

$floor(E\ e)$获取小于等于e的第一个元素,**找不到返回null**

$lower(E\ e)$获取小于e的第一个元素,**找不到返回null**

$higher(E\ e)$获取大于e的第一个元素,**找不到返回null**

*****

### TreeMap类

TreeSet类是基于红黑树实现的.

基本方法和Map一致

有几个比较好用的API:

$firstKey()$ 获取有序表中的第一个元素

$lastKey()$ 获取有序表中的最后一个元素

$ceilingKey(E\ e)$获取大于等于e的第一个元素, **找不到返回null**

$floorKey(E\ e)$获取小于等于e的第一个元素,**找不到返回null**

*****

### 集合(位运算)相关

$整数包装类.bitCount()$ 获取该集合中二进制1的个数.

$32 -整数包装类.numberOfLeadingZeros()$ 获取该集合的长度

$31 - 整数包装类.numberOfLeadingZeros()$ 获取该集合的最大元素

$整数包装类.numberOfTrailingZeros$ 获取该整数中的最小元素.



### Map

$merge(key,value,BitFunction<T,V,R>)根据value值与旧值进行计算,并返回新的结果.如果key不存在,则插入value.$

$computeIfAbsent(key,Fuction<T,V>)如果key不存在,则插入执行函数返回的值,并返回该值$

$getOrDefault(key,defaultValue)如果key不存在,则返回默认值$
