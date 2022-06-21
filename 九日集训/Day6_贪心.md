# Day6 贪心

## 1913. 两个数对之间的最大乘积差

### 题目描述

两个数对 (a, b) 和 (c, d) 之间的 乘积差 定义为 (a * b) - (c * d) 。

例如，(5, 6) 和 (2, 7) 之间的乘积差是 (5 * 6) - (2 * 7) = 16 。
给你一个整数数组 nums ，选出四个 不同的 下标 w、x、y 和 z ，使数对 (nums[w], nums[x]) 和 (nums[y], nums[z]) 之间的 乘积差 取到 最大值 。

返回以这种方式取得的乘积差中的 最大值 。

```C
int cmp(int *x,int *y){
    return *x-*y;
}

int maxProductDifference(int* nums, int numsSize){
    qsort(nums,numsSize,sizeof(int),cmp);
    return nums[numsSize-1]*nums[numsSize-2] - nums[0]*nums[1];
}
```



## 976. 三角形的最大周长

### 题目描述

给定由一些正数（代表长度）组成的数组 `nums` ，返回 *由其中三个长度组成的、**面积不为零**的三角形的最大周长* 。如果不能形成任何面积不为零的三角形，返回 `0`。

~~~C
int cmp(int *x,int *y){
    return *x-*y;
}
int largestPerimeter(int* nums, int numsSize){
    qsort(nums,numsSize,sizeof(int),cmp);
    for(int i = numsSize-1;i>=2;i--){
        if(nums[i]<nums[i-1]+nums[i-2]) {
            return nums[i]+nums[i-1]+nums[i-2];
        }
    }
    return 0;
}
~~~



## 561. 数组拆分Ⅰ

### 题目描述

给定长度为 2n 的整数数组 nums ，你的任务是将这些数分成 n 对, 例如 (a1, b1), (a2, b2), ..., (an, bn) ，使得从 1 到 n 的 min(ai, bi) 总和最大。

返回该 最大总和 。

~~~C
int cmp(int *x,int *y){
    return *x-*y;
}

int arrayPairSum(int* nums, int numsSize){
    qsort(nums,numsSize,sizeof(int),cmp);
    int ans = 0;
    for(int i=0;i<numsSize;i+=2){
        ans+=nums[i];
    }
    return ans;
}
~~~



## 881. 救生艇

### 题目描述

给定数组 people 。people[i]表示第 i 个人的体重 ，船的数量不限，每艘船可以承载的最大重量为 limit。

每艘船最多可同时载两人，但条件是这些人的重量之和最多为 limit。

返回 承载所有人所需的最小船数 。

~~~C
int cmp(int *x,int *y){
    return *y-*x;
}

int numRescueBoats(int* people, int peopleSize, int limit){
    qsort(people,peopleSize,sizeof(int),cmp);
    int ans = 0;
    for(int i=0,j=peopleSize-1;i<=j;){
        if(i == j){
            ans++;
            return ans;
        }
        if(people[i]+people[j]<=limit){
            ans++;
            j--,i++;
        }
        else{
            ans++;
            i++;
        }
    }
    return ans;
}
~~~

> 难度在于中间的i和j相遇之后的处理方式，我想了半天才解决掉

## 324. 摆动排序Ⅱ

### 题目描述

给你一个整数数组 nums，将它重新排列成 nums[0] < nums[1] > nums[2] < nums[3]... 的顺序。

你可以假设所有输入数组都可以得到满足题目要求的结果。

~~~C
int cmp(int *x, int *y){
    return *x-*y;
}

void wiggleSort(int* nums, int numsSize){
    int *ans = (int*)malloc(sizeof(int)*numsSize);
    qsort(nums,numsSize,sizeof(int),cmp);
    for(int i=numsSize/2-1;i>=0;i--){
        if(numsSize%2==0){
            ans[2*(numsSize/2-i-1)] = nums[i];
            ans[2*(numsSize/2-i-1)+1] = nums[i+numsSize/2];
        }
        else{
            ans[2*(numsSize/2-i-1)] = nums[i];
            ans[2*(numsSize/2-i-1)+1] = nums[numsSize/2+1+i];
        }
    }
    if(numsSize%2==1){
        ans[numsSize-1] = ans[0];
        ans[0] = nums[numsSize/2];
        //ans[numsSize-1] = nums[numsSize/2];
    }
    for(int j=0;j<numsSize;j++){
        nums[j]=ans[j];
    }
    
}
~~~

> 半成品，纠结了快1个小时还是有5个例程过不去，直接过了吧

## 455. 分发饼干

### 题目描述

假设你是一位很棒的家长，想要给你的孩子们一些小饼干。但是，每个孩子最多只能给一块饼干。

对每个孩子 i，都有一个胃口值 g[i]，这是能让孩子们满足胃口的饼干的最小尺寸；并且每块饼干 j，都有一个尺寸 s[j] 。如果 s[j] >= g[i]，我们可以将这个饼干 j 分配给孩子 i ，这个孩子会得到满足。你的目标是尽可能满足越多数量的孩子，并输出这个最大数值。

~~~C
int cmp(int *x, int *y){
    return *y-*x;
}

int findContentChildren(int* g, int gSize, int* s, int sSize){
    if(gSize == 0 || sSize == 0) return 0;
    if(gSize>=2) qsort(g,gSize,sizeof(int),cmp);
    if(sSize>=2) qsort(s,sSize,sizeof(int),cmp);

    int ans = 0;
    
    for(int i=0,j=0;i<sSize && j<gSize;j++){
        if(s[i]>=g[j]){
            ans++;
            i++;
        }
    }
    return ans;
}
~~~

> for语句中间的判断条件只能使用一个表达式

## 1827. 最少操作数使数组递增

### 题目描述

给你一个整数数组 nums （下标从 0 开始）。每一次操作中，你可以选择数组中一个元素，并将它增加 1 。

比方说，如果 nums = [1,2,3] ，你可以选择增加 nums[1] 得到 nums = [1,3,3] 。
请你返回使 nums 严格递增 的 最少 操作次数。

我们称数组 nums 是 严格递增的 ，当它满足对于所有的 0 <= i < nums.length - 1 都有 nums[i] < nums[i+1] 。一个长度为 1 的数组是严格递增的一种特殊情况。

~~~C
int minOperations(int* nums, int numsSize){
    int ans = 0;
    if(numsSize == 1) return 0;
    for(int i=1;i<numsSize;i++){
       while(nums[i]<=nums[i-1]){
           nums[i]+=1;
           ans++;
       }
    }
    return ans;
}
~~~



## 945. 使数组递增的最小增量

### 题目描述

给你一个整数数组 nums 。每次 move 操作将会选择任意一个满足 0 <= i < nums.length 的下标 i，并将 nums[i] 递增 1。

返回使 nums 中的每个值都变成唯一的所需要的最少操作次数。

~~~C
int cmp(int *x, int *y){
    return *x-*y;
}

int minIncrementForUnique(int* nums, int numsSize){
    int ans = 0;
    if(numsSize == 1) return 0;
    qsort(nums,numsSize,sizeof(int),cmp);
    for(int i=1;i<numsSize;i++){
        while(nums[i]<=nums[i-1]){
            nums[i]+=1;
            ans++;
        }
    }
    return ans;
}
~~~



## 611. 有效三角形的个数

### 题目描述

给定一个包含非负整数的数组 `nums` ，返回其中可以组成三角形三条边的三元组个数。

~~~C
int cmp(int *x,int *y){
    return *x-*y;
}

int triangleNumber(int* nums, int numsSize){
    int ans = 0;
    if(numsSize<3) return 0;
    qsort(nums,numsSize,sizeof(int),cmp);
    int i,j,k;
    for(i=0;i<numsSize-2;i++){
        for(j=i+1;j<numsSize-1;j++){
            for(k=j+1;k<numsSize;k++){
                if(nums[i]+nums[j]<=nums[k]){
                    break;
                }
            }
            ans += k-j-1;
        }
    }
    return ans;
}
~~~

> 亲测能用，但是超出了时间限制哈哈哈哈