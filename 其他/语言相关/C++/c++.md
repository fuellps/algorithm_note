#### vector

##### Element access

- back: access the last element
- front: access the first element

##### Capacity

- empty: check whether the container is empty
- size:  return the number of elements

##### Modifiers

- push_back:  adds an element to the end
- pop_back: removes the last element



##### Example

```c++
#include <iostream>
#include <vector>
 using namespace std;
int main()
{
    vector<int> a{2,3,4,5};
    vector<int> b(10,1);  //开辟长度为10的数组，数组初始化值全为1.
    cout << a.back() << endl;
    for(int x : a) cout << x << " ";
    cout << endl;
}
```

