# Assignment 3 – Set A – Q1(c): Recursive Quick Sort

## Lab-book task
Accept n integers and sort them in ascending order using recursive quick sort.

## Solution
```c
#include <stdio.h>
#include <stdlib.h>

int partition(int a[],int lb,int ub){
    int down=lb,up=ub,pivot=a[lb];
    while(down<up){
        while(down<up&&a[down]<=pivot)down++;
        while(up>down&&a[up]>pivot)up--;
        if(down<up){int t=a[down];a[down]=a[up];a[up]=t;}
    }
    a[lb]=a[up];a[up]=pivot;return up;
}
void quick_sort(int a[],int lb,int ub){if(lb<ub){int j=partition(a,lb,ub);quick_sort(a,lb,j-1);quick_sort(a,j+1,ub);}}
int main(void){int n;printf("Enter n: ");scanf("%d",&n);if(n<=0)return 1;int*a=malloc((size_t)n*sizeof(int));if(!a)return 1;printf("Enter values: ");for(int i=0;i<n;i++)scanf("%d",&a[i]);quick_sort(a,0,n-1);printf("Sorted: ");for(int i=0;i<n;i++)printf("%d ",a[i]);printf("\n");free(a);return 0;}
```
