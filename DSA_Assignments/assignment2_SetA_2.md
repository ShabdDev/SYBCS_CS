# Assignment 2 – Set A – Q1(b): Insertion Sort

## Lab-book task
Create a random array of n integers and sort it in ascending order using insertion sort.

## Solution
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int main(void) {
    int n; printf("Enter n: "); scanf("%d", &n);
    if (n <= 0) return 1;
    int *a = malloc((size_t)n*sizeof(int)); if(!a) return 1;
    srand((unsigned)time(NULL));
    for(int i=0;i<n;i++) a[i]=rand()%100;
    printf("Before: "); for(int i=0;i<n;i++) printf("%d ",a[i]); printf("\n");
    for(int i=1;i<n;i++) {
        int temp=a[i], j=i-1;
        while(j>=0 && temp<a[j]) { a[j+1]=a[j]; j--; }
        a[j+1]=temp;
    }
    printf("After : "); for(int i=0;i<n;i++) printf("%d ",a[i]); printf("\n");
    free(a); return 0;
}
```
