# Day2 循环

## 剑指 offer 64. 求1+2+3+……+n

### 题目描述

求 `1+2+...+n` ，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。



~~~c++
class Solution {
public:
    int sumNums(int n) {
        int i = 1,sum = 0;
        for(;i<=n;i++){
            sum += i;
        };
        return sum;
    }
};
~~~



## 231. 2的幂

### 题目描述

给你一个整数 n，请你判断该整数是否是 2 的幂次方。如果是，返回 true ；否则，返回 false 。

如果存在一个整数 x 使得 n == 2x ，则认为 n 是 2 的幂次方



~~~C++
class Solution {
public:
    bool isPowerOfTwo(int n) {
        if(n <= 0) return false;
        if(n == 1) return true;
        int k = 1;
        for(int i = 1;i < 31;i++){
            k *= 2;
            if (k == n) return true;
            if (k > n) return false;
        }
        return false;
    };
};
~~~



## 326. 3的幂

### 题目描述

给定一个整数，写一个函数来判断它是否是 3 的幂次方。如果是，返回 true ；否则，返回 false 。

整数 n 是 3 的幂次方需满足：存在整数 x 使得 n == 3x



~~~C++
class Solution {
public:
    bool isPowerOfThree(int n) {
        if(n <= 0) return false;
        if(n == 1) return true;
        int k = 1;
        for(int i = 1;i < 20;i++){
            k *= 3;
            if (k == n) return true;
            if (k > n) return false;
        }
        return false;
    }
};
~~~

## 342. 4的幂

### 题目描述

给定一个整数，写一个函数来判断它是否是 4 的幂次方。如果是，返回 true ；否则，返回 false 。

整数 n 是 4 的幂次方需满足：存在整数 x 使得 n == 4x



~~~C++
class Solution {
public:
    bool isPowerOfFour(int n) {
        if(n <= 0) return false;
        if(n == 1) return true;
        int k = 1;
        for(int i = 1;i < 16;i++){
            k *= 4;
            if (k == n) return true;
            if (k > n) return false;
        }
        return false;
    }
};
~~~



## 1492. n的第k个因子

### 题目描述

给你两个正整数 n 和 k 。

如果正整数 i 满足 n % i == 0 ，那么我们就说正整数 i 是整数 n 的因子。

考虑整数 n 的所有因子，将它们 升序排列 。请你返回第 k 个因子。如果 n 的因子数少于 k ，请你返回 -1 。



~~~C++
class Solution {
public:
    int kthFactor(int n, int k) {
        int count = 0;
        for (int i = 1;i<=n;i++){
            if(n%i == 0) count++;
            if(count == k) return i;
        };
        return -1;
    }
};
~~~


## 367.完全平方数

### 题目描述

给定一个 正整数 num ，编写一个函数，如果 num 是一个完全平方数，则返回 true ，否则返回 false 。

进阶：不要 使用任何内置的库函数，如  sqrt 。



~~~C++
class Solution {
public:
    bool isPerfectSquare(int num) {
        if (num <0) return false;
        if (num == 1) return true;
        if (num == 0) return false;
        for(int i = 1;i < 46341;i++){
            if(i*i == num) return true;
            if(i*i > num) return false;
        }
    return false;
    }
};
~~~

要时刻注意数值的范围，测试用例里面有好几个都是卡在32位边缘出的题目，因为我没有设置边缘条件导致提交失败了四次。