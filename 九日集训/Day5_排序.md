# Day5 排序

## 912. 排序数组

### 题目描述

给你一个整数数组 `nums`，请你将该数组升序排列。

~~~C
 int cmp(void *x,void * y){
    return *(int *)x - *(int *)y;
}
int* sortArray(int* nums, int numsSize, int* returnSize){
    qsort(nums,numsSize,sizeof(int),cmp);
    *returnSize = numsSize;
    return nums;
}
~~~



## 169. 多数元素

### 题目描述

给定一个大小为 n 的数组 nums ，返回其中的多数元素。多数元素是指在数组中出现次数 大于 ⌊ n/2 ⌋ 的元素。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

~~~C
int cmp(void *x,void *y){
    return *(int*)x-*(int*)y;
}
int majorityElement(int* nums, int numsSize){
    qsort(nums,numsSize,sizeof(int),cmp);
    return nums[numsSize/2];
}
~~~



## 217. 存在重复元素

### 题目描述

给你一个整数数组 `nums` 。如果任一值在数组中出现 **至少两次** ，返回 `true` ；如果数组中每个元素互不相同，返回 `false` 。

~~~C
int cmp(void *x,void *y){
    return *(int*)x-*(int*)y;
}
bool containsDuplicate(int* nums, int numsSize){
    qsort(nums,numsSize,sizeof(int),cmp);
    for(int i=0;i<numsSize-1;i++){
        if(nums[i] == nums[i+1]){
            return true;
        }
    }
    return false;
}
~~~



## 164. 最大间距

### 题目描述

给定一个无序的数组 `nums`，返回 *数组在排序之后，相邻元素之间最大的差值* 。如果数组元素个数小于 2，则返回 `0` 。

~~~C
int cmp(void *x,void *y){
    return *(int*)x-*(int*)y;
}
int maximumGap(int* nums, int numsSize){
    qsort(nums,numsSize,sizeof(int),cmp);
    int max = 0;
    if (numsSize<2) return 0;
    for(int i=0;i<numsSize-1;i++){
        if(abs(nums[i]-nums[i+1])>max) 
            max = abs(nums[i]-nums[i+1]);
    }
    return max;
}
~~~



## 905. 按奇偶排序数组

### 题目描述

给你一个整数数组 `nums`，将 `nums` 中的的所有偶数元素移动到数组的前面，后跟所有奇数元素。

返回满足此条件的 **任一数组** 作为答案。

~~~C
int cmp(int *x,int *y){
    return (*x)%2-(*y)%2;
}
int* sortArrayByParity(int* nums, int numsSize, int* returnSize){
    for(int i=0;i<numsSize-1;i++){
        if(nums[i]%2-nums[i+1]%2>0){
            qsort(nums,numsSize,sizeof(int),cmp);
        }
    }
    *returnSize = numsSize;
    return nums;
}
~~~



## 539. 最小时间差

### 题目描述

给定一个 24 小时制（小时:分钟 **"HH:MM"**）的时间列表，找出列表中任意两个时间的最小时间差并以分钟数表示。

~~~C
int cmp(int *x,int *y){
    return *x-*y;
}
int min(int a,int b){
    return a<b?a:b;
}
int findMinDifference(char ** timePoints, int timePointsSize){
    int *ret = (int*)malloc(sizeof(int)*timePointsSize);
    int a,b;
    for(int i=0;i<timePointsSize;i++){
        sscanf(timePoints[i],"%d:%d",&a,&b);
        ret[i] = a * 60 + b;
    }
    qsort(ret,timePointsSize,sizeof(int),cmp);
    int ans = 1440;
    int max = 1440;
    int d = 0;
    for(int j=0;j<timePointsSize-1;j++){
        d = ret[j+1]-ret[j];
        if(d>720 && max-d<ans){
            ans = max-d;
        }
        else{
            if(d<ans){
                ans = d;
            }
        }
    }
    ans = min(ans,ret[0]-ret[timePointsSize-1]+max);
    return ans;
}
~~~

