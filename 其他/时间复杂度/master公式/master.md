标准形式:

$T(N) = a \times T(\frac{N}{b}) + O(n^c)$

1.如果 $\log_b{a} > c$, 那么时间复杂度为$O(N^{\log_b{a}})$

2.如果 $\log_b{a} < c$, 那么时间复杂度为$O(N^c)$

3.如果 $\log_b{a} == c$, 那么时间复杂度为$O(N^{c}\times \log{n})$

补充:$T(N) = 2 \times T(\frac{N}{2}) + O(n\log{n})$的时间复杂度为$O(n\times(\log{n})^2)$