在数组中找到最近x的数

```java
int search(int[] nums,int x){
    int n = nums.length;
    int l = -1, r = n;
    while(l + 1 < r){
        int mid = (l + r) >>> 1;
        if(nums[mid] < x){
            l = mid;
        }else{
            r = mid;
        }
    }
    //上面找到>=x的第一个数
    if(r == n) return nums[n-1]; //数组内都是小于x的数,返回nums[n-1]
    if(r == 0) return nums[0]; //数组内都是>=x的数,返回nums[0]
    return nums[r] - x > x - nums[l] ? nums[l] : nums[r];//哪个绝对值差值小返回哪个数
}
```

如果只需要计算差值的话,可以直接返回最小绝对差

```java
int search(int[] nums,int x){
    int n = nums.length;
    int l = -1, r = n;
    while(l + 1 < r){
        int mid = (l + r) >>> 1;
        if(nums[mid] < x){
            l = mid;
        }else{
            r = mid;
        }
    }
    //上面找到>=x的第一个数
    if(r == n) return x - nums[n-1]; //数组内都是小于x的数,返回nums[n-1]
    if(r == 0) return nums[0] - x; //数组内都是>=x的数,返回nums[0]
    return Math.min(nums[r] - x , x - nums[l]);//返回最小绝对查
}
```

