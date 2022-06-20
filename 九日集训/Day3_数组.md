# Day3 数组

## 33. 搜索旋转排序数组

### 题目描述

整数数组 nums 按升序排列，数组中的值 互不相同 。

在传递给函数之前，nums 在预先未知的某个下标 k（0 <= k < nums.length）上进行了 旋转，使数组变为 [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]（下标 从 0 开始 计数）。例如， [0,1,2,4,5,6,7] 在下标 3 处经旋转后可能变为 [4,5,6,7,0,1,2] 。

给你 旋转后 的数组 nums 和一个整数 target ，如果 nums 中存在这个目标值 target ，则返回它的下标，否则返回 -1 。



~~~C++
class Solution {
public:
    int search(vector<int>& nums, int target) {
        //int l = sizeof(nums)/sizeof(nums[0]);
        int l = end(nums)-begin(nums);
        for(int i = 0;i<l;i++){
            if(nums[i] == target) {
                return i;
            }
        }
    return -1;
    }
};
~~~

> 这里的sizeof不能用是因为这里的nums是一个模板，不是一个单纯的数组，所以使用sizeof测量的长度与实际有出入。



## 81. 搜索旋转排序数组Ⅱ

### 题目描述

已知存在一个按非降序排列的整数数组 nums ，数组中的值不必互不相同。

在传递给函数之前，nums 在预先未知的某个下标 k（0 <= k < nums.length）上进行了 旋转 ，使数组变为 [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]（下标 从 0 开始 计数）。例如， [0,1,2,4,4,4,5,6,6,7] 在下标 5 处经旋转后可能变为 [4,5,6,6,7,0,1,2,4,4] 。

给你 旋转后 的数组 nums 和一个整数 target ，请你编写一个函数来判断给定的目标值是否存在于数组中。如果 nums 中存在这个目标值 target ，则返回 true ，否则返回 false 。



~~~C++
class Solution {
public:
    bool search(vector<int>& nums, int target) {
        int l = end(nums)-begin(nums);
        for(int i = 0;i<l;i++){
            if(nums[i] == target) {
                return true;
            }
        }
    return false;
    }
};
~~~

> 与上一个题目基本一致



## 153. 寻找旋转排序数组中的最小值

### 题目描述

已知一个长度为 n 的数组，预先按照升序排列，经由 1 到 n 次 旋转 后，得到输入数组。例如，原数组 nums = [0,1,2,4,5,6,7] 在变化后可能得到：
若旋转 4 次，则可以得到 [4,5,6,7,0,1,2]
若旋转 7 次，则可以得到 [0,1,2,4,5,6,7]
注意，数组 [a[0], a[1], a[2], ..., a[n-1]] 旋转一次 的结果为数组 [a[n-1], a[0], a[1], a[2], ..., a[n-2]] 。

给你一个元素值 互不相同 的数组 nums ，它原来是一个升序排列的数组，并按上述情形进行了多次旋转。请你找出并返回数组中的 最小元素 。

~~~C++
class Solution {
public:
    int findMin(vector<int>& nums) {
        int ans = nums[0];
        for (int i = 1;i<end(nums)-begin(nums);i++){
            if(nums[i]<ans) ans = nums[i];
        }
    return ans;
    }
};
~~~



## 70.爬楼梯

### 题目描述

假设你正在爬楼梯。需要 `n` 阶你才能到达楼顶。

每次你可以爬 `1` 或 `2` 个台阶。你有多少种不同的方法可以爬到楼顶呢？

~~~C++
class Solution {
public:
    int climbStairs(int n) {
        int arr[45] = {1,2};
        if(n == 1) return 1;
        if(n == 2) return 2;
        for (int i = 2;i<n;i++){
            arr[i] = arr[i-1]+arr[i-2];
        }
        return arr[n-1];
    }
};
~~~

> 有点脑筋急转弯的意思，其实对每一层起决定作用的只有倒数的两步，因为之前层数的步数都已经计算过了，只要加在一起就行了。



## 509. 斐波那契数列

### 题目描述

斐波那契数 （通常用 F(n) 表示）形成的序列称为 斐波那契数列 。该数列由 0 和 1 开始，后面的每一项数字都是前面两项数字的和。也就是：

F(0) = 0，F(1) = 1
F(n) = F(n - 1) + F(n - 2)，其中 n > 1
给定 n ，请计算 F(n) 。

~~~C++
class Solution {
public:
    int fib(int n) {
        int F[31] = {0,1};
        
        for(int i = 2;i<n+1;i++){
            F[i] = F[i-1]+F[i-2];
        }
        return F[n];
    }
};
~~~



## 1137. 第n个泰波那契数

### 题目描述

泰波那契序列 Tn 定义如下： 

T0 = 0, T1 = 1, T2 = 1, 且在 n >= 0 的条件下 Tn+3 = Tn + Tn+1 + Tn+2

给你整数 n，请返回第 n 个泰波那契数 Tn 的值。

~~~C++
class Solution {
public:
    int tribonacci(int n) {
        int T[38] = {0,1,1};
        for(int i=3;i<n+1;i++){
            T[i] = T[i-1]+T[i-2]+T[i-3];
        }
        return T[n];
    }
};
~~~





## 2006. 差的绝对值数目为k的数对数目

### 题目描述

给你一个整数数组 nums 和一个整数 k ，请你返回数对 (i, j) 的数目，满足 i < j 且 |nums[i] - nums[j]| == k 。

|x| 的值定义为：

如果 x >= 0 ，那么值为 x 。
如果 x < 0 ，那么值为 -x 。

~~~C++
class Solution {
public:
    int countKDifference(vector<int>& nums, int k) {
        int l = end(nums)-begin(nums);
        int count = 0;
        for (int i = 0;i<l-1;i++){
            for (int j = i+1;j<l;j++){
                if(abs(nums[i]-nums[j]) == k) count++;
            };
        };
        return count;
    };
};
~~~





## LCP 01.猜数字

### 题目描述

小A 和 小B 在玩猜数字。小B 每次从 1, 2, 3 中随机选择一个，小A 每次也从 1, 2, 3 中选择一个猜。他们一共进行三次这个游戏，请返回 小A 猜对了几次？

输入的guess数组为 小A 每次的猜测，answer数组为 小B 每次的选择。guess和answer的长度都等于3

~~~C++
class Solution {
public:
    int game(vector<int>& guess, vector<int>& answer) {
        int l = end(guess)-begin(guess);
        int count = 0;
        for(int i = 0;i<l;i++){
            if(guess[i] == answer[i]) count++;           
        }
        return count;
    }
};
~~~



## LCP 06.拿硬币

### 题目描述

桌上有 `n` 堆力扣币，每堆的数量保存在数组 `coins` 中。我们每次可以选择任意一堆，拿走其中的一枚或者两枚，求拿完所有力扣币的最少次数。

~~~C++
class Solution {
public:
    int minCount(vector<int>& coins) {
        int l = end(coins)-begin(coins);
        int count = 0;
        int c = 0;
        for(int i = 0;i<l;i++){
            c = coins[i]/2 +coins[i]%2;
            count += c;
        }
        return count;
    }
};
~~~





## 剑指offerⅡ 069. 山峰数组的顶部

### 题目描述

符合下列属性的数组 arr 称为 山峰数组（山脉数组） ：

arr.length >= 3
存在 i（0 < i < arr.length - 1）使得：
arr[0] < arr[1] < ... arr[i-1] < arr[i]
arr[i] > arr[i+1] > ... > arr[arr.length - 1]
给定由整数组成的山峰数组 arr ，返回任何满足 arr[0] < arr[1] < ... arr[i - 1] < arr[i] > arr[i + 1] > ... > arr[arr.length - 1] 的下标 i ，即山峰顶部。

~~~C++
class Solution {
public:
    int peakIndexInMountainArray(vector<int>& arr) {
        for(int i = 0;;i++){
            if(arr[i+1]<arr[i]) return i;
        }
    }
};
~~~



