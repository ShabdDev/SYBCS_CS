# Assignment 3 – Set C – Q1: Random Pivot in Quick Sort

## Lab-book task
Explain how to choose the pivot randomly instead of always choosing the first element.

## Solution
Generate a random index between `lb` and `ub`, swap that element with `A[lb]`, and then execute the workbook partition algorithm.

```c
int p = lb + rand() % (ub - lb + 1);
int t = A[lb]; A[lb] = A[p]; A[p] = t;
/* now A[lb] is the random pivot */
```

Call `srand((unsigned)time(NULL));` once in `main`.
