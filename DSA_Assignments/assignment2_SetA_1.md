# Assignment 2 – Set A – Q1(a): Bubble Sort

## Lab-book task
Sort a random array of n integers in ascending order using bubble sort.

## Solution
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int main(void) {
    int n;
    printf("Enter n: "); scanf("%d", &n);
    if (n <= 0) return 1;
    int *a = malloc((size_t)n * sizeof(int));
    if (!a) return 1;
    srand((unsigned)time(NULL));
    for (int i = 0; i < n; i++) a[i] = rand() % 100;

    printf("Before: "); for (int i=0;i<n;i++) printf("%d ",a[i]); printf("\n");
    for (int i=0;i<n-1;i++) {
        int swapped=0;
        for (int j=0;j<n-i-1;j++) {
            if (a[j] > a[j+1]) { int t=a[j]; a[j]=a[j+1]; a[j+1]=t; swapped=1; }
        }
        if (!swapped) break;
    }
    printf("After : "); for (int i=0;i<n;i++) printf("%d ",a[i]); printf("\n");
    free(a); return 0;
}
```
