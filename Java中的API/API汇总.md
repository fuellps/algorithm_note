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
