# Day4 指针

## 1470. 重新排列数组

### 题目描述

给你一个数组 nums ，数组中有 2n 个元素，按 [x1,x2,...,xn,y1,y2,...,yn] 的格式排列。

请你将数组按 [x1,y1,x2,y2,...,xn,yn] 格式重新排列，返回重排后的数组。

~~~C++
class Solution {
public:
    vector<int> shuffle(vector<int>& nums, int n) {
        int* ret = (int *)malloc(sizeof(int)*2*n);
        for(int i = 0;i<n;i++){
            ret[2*i] = nums[i];
            ret[2*i+1] = nums[i+n];
        }
        for(int j = 0;j<2*n;j++){
            nums[j] = ret[j];
        }
        return nums;
    }
};
~~~





## 1929. 数组串联

### 题目描述

给你一个长度为 n 的整数数组 nums 。请你构建一个长度为 2n 的答案数组 ans ，数组下标 从 0 开始计数 ，对于所有 0 <= i < n 的 i ，满足下述所有要求：

ans[i] == nums[i]
ans[i + n] == nums[i]
具体而言，ans 由两个 nums 数组 串联 形成。

返回数组 ans 。

~~~C
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* getConcatenation(int* nums, int numsSize, int* returnSize){
    int* ret = (int*)malloc(sizeof(int)*2*numsSize);
    for(int i = 0;i<numsSize;i++){
        ret[i] = ret[i+numsSize] = nums[i];
    }
    *returnSize = 2*numsSize;
    return ret;
}
~~~



## 1920. 基于排列构建数组

### 题目描述

给你一个 从 0 开始的排列 nums（下标也从 0 开始）。请你构建一个 同样长度 的数组 ans ，其中，对于每个 i（0 <= i < nums.length），都满足 ans[i] = nums[nums[i]] 。返回构建好的数组 ans 。

从 0 开始的排列 nums 是一个由 0 到 nums.length - 1（0 和 nums.length - 1 也包含在内）的不同整数组成的数组。

~~~C
int* buildArray(int* nums, int numsSize, int* returnSize){
    int *ans = (int*)malloc(sizeof(int)*numsSize);
    for(int i=0;i<numsSize;i++){
        ans[i] = nums[nums[i]];
    }
    *returnSize = numsSize;
    return ans;
}
~~~







## 1480. 一维数组的动态和

### 题目描述

给你一个数组 nums 。数组「动态和」的计算公式为：runningSum[i] = sum(nums[0]…nums[i]) 。

请返回 nums 的动态和

~~~C
int* runningSum(int* nums, int numsSize, int* returnSize){
    if(numsSize==1) return nums[0];
    for(int i=1;i<numsSize;i++){
        nums[i] = nums[i]+nums[i-1];
    }
    *returnSize = numsSize;
    return nums;
}
~~~



## 剑指offer 58. 左旋转字符串

### 题目描述

字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。

~~~C
char* reverseLeftWords(char* s, int n){
    char* tmp = (char*)malloc(sizeof(char)*n);
    for(int i=0;i<n;i++){
        tmp[i] = s[i];
    }
    int l = strlen(s);
    for(int j=0;j<l-n;j++){
        s[j] = s[j+n];
    }
    for(int k=0;k<n;k++){
        s[l-n+k] = tmp[k];
    }
    return s;
}
~~~



## 1108. ip地址无效化

### 题目描述

给你一个有效的 [IPv4](https://baike.baidu.com/item/IPv4) 地址 `address`，返回这个 IP 地址的无效化版本。

所谓无效化 IP 地址，其实就是用 `"[.]"` 代替了每个 `"."`。

~~~C
char * defangIPaddr(char * address){
    char* ans = (char*)malloc(sizeof(char)*1000);
    int i,k;
    for(i=0,k=0;address[i];i++,k++){
        if(address[i]!='.') 
            ans[k] = address[i];
        else{
            ans[k++] = '[';
            ans[k++] = '.';
            ans[k] = ']';
        } 
    }
    ans[k] = '\0';
    return ans;
}
~~~





## 剑指offer 05. 替换空格

### 题目描述

请实现一个函数，把字符串 `s` 中的每个空格替换成"%20"。

~~~C
char* replaceSpace(char* s){
    char* ans = (char*)malloc(sizeof(char)*20000);
    int i,k;
    for(i=0,k=0;s[i];i++,k++){
        if(s[i]!=' ') 
            ans[k] = s[i];
        else{
            ans[k++] = '%';
            ans[k++] = '2';
            ans[k] = '0';
        } 
    }
    ans[k] = '\0';
    return ans;
}
~~~



