# Day8 二维指针

## 832. 翻转图像

### 题目描述

给定一个 n x n 的二进制矩阵 image ，先 水平 翻转图像，然后 反转 图像并返回 结果 。

水平翻转图片就是将图片的每一行都进行翻转，即逆序。

例如，水平翻转 [1,1,0] 的结果是 [0,1,1]。
反转图片的意思是图片中的 0 全部被 1 替换， 1 全部被 0 替换。

例如，反转 [0,1,1] 的结果是 [1,0,0]。

~~~C
int **myMatrix(int r,int c,int *returnSize,int **returnColumnSize){
    int **ret = (int**)malloc(sizeof(int*)*r);
    *returnColumnSize = (int*)malloc(sizeof(int)*r);
    *returnSize = r;
    for(int i=0;i<r;i++){
        ret[i] = (int*)malloc(sizeof(int)*c);
        (*returnColumnSize)[i] = c;
    }
    return ret;    
}
int** flipAndInvertImage(int** image, int imageSize, int* imageColSize, int* returnSize, int** returnColumnSizes){
    
    int i,j;
    int c = imageColSize[0];
    int** ret = myMatrix(r,c,returnSize,returnColumnSizes);

    for(i=0;i<r;i++){
        for(j=0;j<c;j++){
            ret[i][j] = 1-image[i][c-j-1];
        }
    }
    return ret;
}
~~~



## 867. 转置矩阵

### 题目描述

给你一个二维整数数组 `matrix`， 返回 `matrix` 的 **转置矩阵** 。

矩阵的 **转置** 是指将矩阵的主对角线翻转，交换矩阵的行索引与列索引。

~~~C
int **myMatrix(int r,int c,int *returnSize,int **returnColumnSizes){
    int **ret = (int**)malloc(sizeof(int*)*r);
    *returnSize = r;
    *returnColumnSizes = (int*)malloc(sizeof(int)*c);
    for(int i=0;i<r;i++){
        ret[i] = (int*)malloc(sizeof(int)*c);
        (*returnColumnSizes)[i] = c;
    }
    return ret;
}

int** transpose(int** matrix, int matrixSize, int* matrixColSize, int* returnSize, int** returnColumnSizes){
    int tmp;
    int i,j;
    int c = matrixSize;
    int r = matrixColSize[0];
    int **ret = myMatrix(r,c,returnSize,returnColumnSizes);
    for(i=0;i<r;i++){
        for(j=0;j<c;j++){
            ret[i][j] = matrix[j][i];
        }
    }
    return ret;
}
~~~

