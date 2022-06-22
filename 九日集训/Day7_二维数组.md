# 二维数组

## 1351. 统计有序矩阵中的负数

### 题目描述

给你一个 `m * n` 的矩阵 `grid`，矩阵中的元素无论是按行还是按列，都以非递增顺序排列。 请你统计并返回 `grid` 中 **负数** 的数目。



```C
int countNegatives(int** grid, int gridSize, int* gridColSize){
    int r = gridSize;
    int c = *gridColSize;
    int ans = 0;
    int i,j;
    for(i=0;i<r;i++){
        for(j=0;j<c;j++){
            if(grid[i][j]<0){
                ans = ans+c-j;
                break;
            }
        }
    }
    return ans;
}
```

## 1572. 矩阵对角线元素的和

### 题目描述

给你一个正方形矩阵 `mat`，请你返回矩阵对角线元素的和。

请你返回在矩阵主对角线上的元素和副对角线上且不在主对角线上元素的和。

```C
int diagonalSum(int** mat, int matSize, int* matColSize){
    int n = matSize;
    int ans = 0;
    for(int i=0;i<n/2;i++){
        ans = ans+mat[i][i]+mat[i][n-i-1]+mat[n-1-i][i]+mat[n-1-i][n-1-i];
    }
    if(n%2==1){
        ans+=mat[n/2][n/2];
    }
    return ans;
}
```



## 1672. 最富有客户的资产总量

### 题目描述

给你一个 m x n 的整数网格 accounts ，其中 accounts[i][j] 是第 i 位客户在第 j 家银行托管的资产数量。返回最富有客户所拥有的 资产总量 。

客户的 资产总量 就是他们在各家银行托管的资产数量之和。最富有客户就是 资产总量 最大的客户

```C
int maximumWealth(int** accounts, int accountsSize, int* accountsColSize){
    int tmp;
    int ans = 0;
    for(int i=0;i<accountsSize;i++){
        tmp=0;
        for(int j=0;j<*accountsColSize;j++){
            tmp+=accounts[i][j];
        }
        if(tmp>ans) ans = tmp;
    }
    return ans;
}
```

## 766. 托普利兹矩阵

### 题目描述

给你一个 m x n 的矩阵 matrix 。如果这个矩阵是托普利茨矩阵，返回 true ；否则，返回 false 。

如果矩阵上每一条由左上到右下的对角线上的元素都相同，那么这个矩阵是 托普利茨矩阵 。

 ```C
 bool checkEqual(int **matrix,int row,int col,int l_r,int l_c){
     int i,j;
     for(i=row+1,j=col+1;i<l_r && j<l_c;i++,j++){
         if (matrix[i][j] != matrix[i-1][j-1]){
             return false;
         }
     }
     return true;
 }
 
 bool isToeplitzMatrix(int** matrix, int matrixSize, int* matrixColSize){
     bool t;
     for(int i=0;i<*matrixColSize-1;i++){
         t = checkEqual(matrix,0,i,matrixSize,*matrixColSize);
         if(!t){
             return false;
         }
     }
     for(int j=1;j<matrixSize-1;j++){
         t = checkEqual(matrix,j,0,matrixSize,*matrixColSize);
         if(!t){
             return false;
         }
     }
     return true;
 }
 ```



## 1380. 矩阵中的幸运数

### 题目描述

给你一个 m * n 的矩阵，矩阵中的数字 各不相同 。请你按 任意 顺序返回矩阵中的所有幸运数。

幸运数 是指矩阵中满足同时下列两个条件的元素：

在同一行的所有元素中最小
在同一列的所有元素中最大

```C
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* luckyNumbers (int** matrix, int matrixSize, int* matrixColSize, int* returnSize){
    int count = 0;
    int *ans = (int *)malloc(sizeof(int)*50);
    int min,max;
    int index=0;
    if(matrixSize==1){
        min = matrix[0][0];
        for(int x=0;x<*matrixColSize;x++){
            if(matrix[0][x]<min){
                min = matrix[0][x];
            }
        }
        ans[count] = min;
        count++;
        *returnSize = count;
        return ans;
    }
    if(*matrixColSize==1){
        max = matrix[0][0];
        for(int y=0;y<matrixSize;y++){
            if(matrix[y][0]>max){
                max = matrix[y][0];
            }
        }
        ans[count] = max;
        count++;
        *returnSize = count;
        return ans;
    }
    for(int i=0;i<matrixSize;i++){
        for(int j=0;j<*matrixColSize;j++){
            min = matrix[i][0];
            if(matrix[i][j]<min){
                min = matrix[i][j];
                index = j;
            } 
        }
        for(int k=0;k<matrixSize;k++){
            max=matrix[0][index];
            if(max<matrix[k][index]){
                max=matrix[k][index];
            }
        }
        if(max==min){
            ans[count] = max;
            count++;
        }
    }
    *returnSize = count;
    return ans;
}
```

