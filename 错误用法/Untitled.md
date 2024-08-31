```java
List<Integer>[] g = new List[n];
   //     Arrays.fill(g,new ArrayList<>());这是错误的,这样会在g数组中都共用同一个ArrayList,导致下面加边时成为完全图
        Arrays.setAll(g,i->new ArrayList<>());//m
        for(int[] edge : edges){
            g[edge[0]].add(edge[1]);

        }
        for(List<Integer> edge : g){
            System.out.println(edge);
        }
```

