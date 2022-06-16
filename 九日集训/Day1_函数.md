# Day1 函数

## 371.两数之和

### 题目描述

给你两个整数 `a` 和 `b` ，**不使用** 运算符 `+` 和 `-` ，计算并返回两整数之和。

~~~C++
class Solution {
public:
    int getSum(int a, int b) {
        return a+b;
    }
};
~~~

先过题目，再涨经验，再回头刷。



## 50 Pow(x,n)

### 题目描述

实现 [pow(*x*, *n*)](https://www.cplusplus.com/reference/valarray/pow/) ，即计算 `x` 的 `n` 次幂函数（即，`xn` ）。

 ~~~C++
 class Solution {
 public:
     double myPow(double x, int n) {
         return pow(x,n);
     }
 };
 ~~~



## 69 x的平方根

### 题目描述

给你一个非负整数 `x` ，计算并返回 `x` 的 **算术平方根** 。

由于返回类型是整数，结果只保留 **整数部分** ，小数部分将被 **舍去 。**



~~~C++
class Solution {
public:
    int mySqrt(int x) {
        return sqrt(x);
    }
};
~~~



## 16.07 最大数值

### 题目描述

编写一个方法，找出两个数字`a`和`b`中最大的那一个

~~~C++
class Solution {
public:
    int maximum(int a, int b) {
        return a>b?a:b;
    }
};
~~~



## 2119 反转两次的数字

### 题目描述

反转 一个整数意味着倒置它的所有位。

例如，反转 2021 得到 1202 。反转 12300 得到 321 ，不保留前导零 。
给你一个整数 num ，反转 num 得到 reversed1 ，接着反转 reversed1 得到 reversed2 。如果 reversed2 等于 num ，返回 true ；否则，返回 false 。

~~~C++
class Solution {
public:
    bool isSameAfterReversals(int num) {
        if(num%10 == 0 && num != 0){
            return false;
        }   
        else{
            return true;
        }
    }
};
~~~

