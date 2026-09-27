# Assignment 3 – Set A – Q1(a): Counting Sort

## Lab-book task
Accept n integers and sort them in ascending order using counting sort.

## Solution
```c
#include <stdio.h>
#include <stdlib.h>

int main(void) {
    int n; printf("Enter n: "); scanf("%d", &n); if(n<=0)return 1;
    int *a=malloc((size_t)n*sizeof(int)); if(!a)return 1;
    printf("Enter %d non-negative integers: ",n);
    int max=0; for(int i=0;i<n;i++){scanf("%d",&a[i]);if(a[i]<0){printf("Use non-negative integers.\n");free(a);return 1;}if(a[i]>max)max=a[i];}
    int *count=calloc((size_t)max+1,sizeof(int)); if(!count){free(a);return 1;}
    for(int i=0;i<n;i++)count[a[i]]++;
    int k=0; for(int v=0;v<=max;v++)while(count[v]--)a[k++]=v;
    printf("Sorted: ");for(int i=0;i<n;i++)printf("%d ",a[i]);printf("\n");
    free(count);free(a);return 0;
}
```

## Notes / assumptions
The workbook describes counting sort as part of Assignment 3 and calls the algorithms “recursive”; standard counting sort itself is non-recursive. This implementation follows the counting-sort algorithm given in the workbook.
