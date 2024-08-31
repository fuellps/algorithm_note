

```c++
#include <bits/stdc++.h>
using namespace std;

const int N = 110;
double a[N][N];//系数矩阵
int n;
double esp = 1e-6;//精度
int gas(){
    int r,c;
    for( c = 0,r = 0; c < n; c++){
        int t = r;
        
        for(int i = r; i < n; i++){
            if(fabs(a[i][c]) > fabs(a[t][c])) t = i; //找到当前列最大的值
        }
    
    
        if(fabs(a[t][c]) < esp) continue;//当前列最大值为0,要么无解要么无穷多组解
        for(int j = c; j <= n; j++) swap(a[r][j], a[t][j]); //交换两行的值
        for(int j = n; j >= c; j--) a[r][j] /= a[r][c];//将当前行第1个数变成1
        for(int i = r + 1; i < n; i++){//从下一行开始,将当前列的值都置为0
            if(fabs(a[i][c]) < esp) continue;
            for(int j = n; j >= c; j--){
                    a[i][j] -= a[r][j]* a[i][c]; //当前行减去当前选中列的值为1的行每一个数*当前行第c列的数
            }
        }
        r++;
    }
    if(r < n){
        for(int i = r; i < n; i++){
            if(fabs(a[i][n]) > esp) return 2;
        }
        return 1;
    }
    for(int i = n-1; i >= 0; i--){
        for(int j = i + 1; j < n; j++){
            //解方程组
            a[i][n] -= a[i][j]*a[j][n];
        }
    }
    return 0;
}
int main(){
    cin >> n;
    for(int i = 0; i < n; i++){
        for(int j = 0; j<= n; j++){
             cin >> a[i][j];
        }
    }
    int res = gas();
    if(res == 1){ //无穷多组解
        cout << "Infinite group solutions" << endl;
    }else if(res == 2){//无解
        cout << "No solution" << endl;
    }else{
        for(int i = 0; i < n; i++){//有唯一解
            // cout << a[i][n] << endl;
            printf("%.2f\n", a[i][n]);
        }
    }
}
```

