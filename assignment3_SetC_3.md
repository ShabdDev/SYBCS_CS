# Assignment 3 – Set C – Q3: Merge Sort Descending

## Lab-book task
Explain the modification required for merge sort to sort descending.

## Solution
During merge, select the larger front element first. Change the ascending comparison `a[i] <= a[j]` to `a[i] >= a[j]`. The recursive split and merge structure is unchanged.
