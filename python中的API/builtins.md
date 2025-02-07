### 序列操作相关
> len(x) 返回序列x长度

> range(start = 0,end,step=1) 返回从start到end-1,步长为step的range对象

> zip(*iterable) 接收多个可迭代序列,将每个序列的元素合并为1个元组,多个可迭代序列取长度最短.

> sorted(iterable,key=None,reversed = False) 返回可迭代序列排序后的列表

> enumerate(iterable,start = 0)遍历可迭代对象,返回一个下标从start递增与对应值的元素的元组 

> sum(iterable,start = 0) 返回从start开始,数字形式的可迭代序列之和

> min(*iterable,key=None) 返回可迭代对象的最小值

> max(*iterable,key) 返回可迭代对象的最大值

### 字符串操作相关

> repr() 返回一个字符串在程序解释器中的样子

>str() 返回数据的字符串表示形式

> ord() 将字符串转化为对应的unicode编码值

> chr() 将数字对应的Unicode编码值转化为字符串

### 整数操作相关

> abs() 返回数字的绝对值

> bin() 返回数字的二进制字符串形式 := 0bxxxxx

> pow(a,b,mod=None) 返回$a^b$,如果为*整数且指定mod,已经实现高效的快速幂算法*

> round(x,ndigits=None) 返回x以小数点后ndigits位精度四舍五入后的结果,不指定ndigits默认四舍五入为最接近的整数 
