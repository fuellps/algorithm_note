### 竞赛一些技巧

参见https://www.luogu.com.cn/article/uuh1asja

### 	库函数

#### climits:定义了最值常量

- int最大/小值：INT_MAX, INT_MIN
- long long 最大/小值： LLONG_MAX,LLONG_MI



#### 有些好用的库函数

- reverse(*iter_start, *iter_end)
- fill(*it_start, *iter_end, value)
- copy(*source_start, *source_end,  &destination)
- to_string() 将数字转字符串
- stoi()字符串转数字  stoi(str,nullptr,2) 以2进制形式将字符串转化为数字

> 上面是转化为int，还有其他类型：如stoll转long long,stod转double

##### 最值相关

- max_element(start,end)在[start,end)范围找最大值
- min_element(start,end)在[start,end)范围找最小值

### STL及string

#### set

- `find(x)` 在 `set` 内存在键为 x 的元素时会返回该元素的迭代器，否则返回 `end()`。
- `lower_bound(x)` 返回指向首个不小于给定键的元素的迭代器。如果不存在这样的元素，返回 `end()`。
- `upper_bound(x)` 返回指向首个大于给定键的元素的迭代器。如果不存在这样的元素，返回 `end()`。
- `count(x)` 返回 `set` 内键为 x 的元素数量。

##### Example

```c++
```



#### map

- `erase(key)` 函数会删除键为 `key` 的 **所有** 元素。返回值为删除元素的数量。
- `erase(pos)`: 删除迭代器为 pos 的元素，要求迭代器必须合法。
- `find(x)`: 若容器内存在键为 x 的元素，会返回该元素的迭代器；否则返回 `end()`。
- `lower_bound(x)`: 返回指向首个不小于给定键的元素的迭代器。
- `upper_bound(x)`: 返回指向首个大于给定键的元素的迭代器。若容器内所有元素均小于或等于给定键，返回 `end()`。

##### Example

```c++
int main(){
    map<int,int> mp;
    mp[1] = 3; //赋值
    int x = 666;
    if(mp.find(x) != mp.end()) cout << x << " in map" << endl;
    else cout << x << " not in map" << endl;
    mp[x] = 1;
    //获取map中第一个元素和最后一个元素
    cout << (*mp.begin()).first << " " (*prev(mp.end())).first << endl; /
}
```





#### vector

###### Element access

- back: access the last element
- front: access the first element

###### Capacity

- empty: check whether the container is empty
- size:  return the number of elements

###### Modifiers

- push_back:  adds an element to the end
- pop_back: removes the last element
- insert



##### Example

```c++
#include <iostream>
#include <vector>
 using namespace std;
 
 ostream& operator<<(ostream& os,const vector<int>& a){
 	for(int i = 0;i + 1  < a.size();i++) os << a[i]<< " ";
 	os << a.back();
 }
int main()
{
    vector<int> a{2,3,4,5};
    vector<int> b(10,1);  //开辟长度为10的数组，数组初始化值全为1.
    cout << a.back() << endl; //最后一个元素
    for(int x : a) cout << x << " ";
    cout << endl;
    a.insert(a.begin(),b.begin(),b.end()); //在数组a开头插入b的所有元素
    a.insert(a.end(),666); //在数组a结尾插入元素666
    cout<<a << endl;
}
```

#### string

- substr(pos,len): 截取从pos处开始长度为len的子串
- c_str():转化为c风格的字符串形式。 **用printf函数%s需c风格的字符串.**
- find(tar):查找tar字符串是否存在s中。 **找不到返回s.npos**

### 知识点

#### 运算符重载

> 重载运算符分为两种情况，重载为成员函数或非成员函数。

1. 当重载为成员函数时，因为隐含一个指向当前成员的 `this` 指针作为参数，此时函数的参数个数与运算操作数相比少一个。
2. 而当重载为非成员函数时，函数的参数个数与运算操作数相同。



重载的运算符是带有特殊名称的函数，函数名是由 **operator**和其后要重载的运算符符号构成的。与其他函数一样，重载运算符有 **一个返回类型和参数列表**。

```c++
mat operator* (const mat& mt) const{
    mat res;
    //Todo..
    return res;
}
```

#### IIFE

参见 https://www.cppstories.com/2016/11/iife-for-complex-initialization/

```c++
auto init = []{
    //initize 
    reutrn 0;
}(); //call!
```

