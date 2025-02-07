并查集是一种以森林的形式代表集合,每个集合都以根节点为代表.

```python
fa = list(range(n+1)) # 并查集节点数组
def find(x):
    if x != fa[x]:
        fa[x] = find(fa[x]) #路径压缩
    return fa[x]

def same(x,y): #判断x与y的集合是否相等
    return find(x) == find(y)
def union(x,y): #合并x与y所在的集合
    f
```

