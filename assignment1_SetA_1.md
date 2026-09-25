# Assignment 1 – Set A – Q1(a): Linear Search

## Lab-book task
Create a random array of n integers, accept x, use linear search, and print its position if present.

## Solution
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int main(void) {
    int n, x, i, pos = -1;
    printf("Enter n: ");
    scanf("%d", &n);

    if (n <= 0) { printf("Invalid size.\n"); return 1; }
    int *a = malloc((size_t)n * sizeof(int));
    if (!a) { printf("Memory allocation failed.\n"); return 1; }

    srand((unsigned)time(NULL));
    for (i = 0; i < n; i++) a[i] = rand() % 100;

    printf("Random array: ");
    for (i = 0; i < n; i++) printf("%d ", a[i]);
    printf("\nEnter value to search: ");
    scanf("%d", &x);

    for (i = 0; i < n; i++) {
        if (a[i] == x) { pos = i; break; }
    }

    if (pos != -1) printf("Required number is found at location %d.\n", pos + 1);
    else printf("Required data not found.\n");

    free(a);
    return 0;
}
```

## Notes / assumptions
The workbook specifies random integers in the range 0–99. The reported location is 1-based, matching the workbook algorithm.
