# Assignment 3 – Set A – Q1(b): Recursive Merge Sort

## Lab-book task
Create a random array of n integers and sort it using recursive merge sort.

## Solution
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

void merge(int a[], int low, int mid, int high) {
    int n=high-low+1, *b=malloc((size_t)n*sizeof(int)); if(!b)exit(1);
    int i=low,j=mid+1,k=0;
    while(i<=mid&&j<=high)b[k++]=(a[i]<=a[j])?a[i++]:a[j++];
    while(i<=mid)b[k++]=a[i++]; while(j<=high)b[k++]=a[j++];
    for(i=low,k=0;i<=high;i++,k++)a[i]=b[k];
    free(b);
}
void merge_sort(int a[],int low,int high){
    if(low<high){int mid=low+(high-low)/2;merge_sort(a,low,mid);merge_sort(a,mid+1,high);merge(a,low,mid,high);}
}
int main(void){int n;printf("Enter n: ");scanf("%d",&n);if(n<=0)return 1;int*a=malloc((size_t)n*sizeof(int));if(!a)return 1;srand((unsigned)time(NULL));for(int i=0;i<n;i++)a[i]=rand()%100;printf("Before: ");for(int i=0;i<n;i++)printf("%d ",a[i]);printf("\n");merge_sort(a,0,n-1);printf("After : ");for(int i=0;i<n;i++)printf("%d ",a[i]);printf("\n");free(a);return 0;}
```
