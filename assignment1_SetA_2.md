# Assignment 1 – Set A – Q1(b): Binary Search

## Lab-book task
Accept n sorted values, accept x, use binary search, and print its position if present.

## Solution
```c
#include <stdio.h>
#include <stdlib.h>

int main(void) {
    int n, x;
    printf("Enter n: ");
    scanf("%d", &n);
    if (n <= 0) { printf("Invalid size.\n"); return 1; }

    int *a = malloc((size_t)n * sizeof(int));
    if (!a) { printf("Memory allocation failed.\n"); return 1; }

    printf("Enter %d values in sorted ascending order:\n", n);
    for (int i = 0; i < n; i++) scanf("%d", &a[i]);

    printf("Enter value to search: ");
    scanf("%d", &x);

    int low = 0, high = n - 1, pos = -1;
    while (low <= high) {
        int middle = low + (high - low) / 2;
        if (a[middle] == x) { pos = middle; break; }
        if (x < a[middle]) high = middle - 1;
        else low = middle + 1;
    }

    if (pos != -1) printf("Required number is found at location %d.\n", pos + 1);
    else printf("Required number is not found.\n");

    free(a);
    return 0;
}
```

## Notes / assumptions
Binary search requires the input array to be sorted.
