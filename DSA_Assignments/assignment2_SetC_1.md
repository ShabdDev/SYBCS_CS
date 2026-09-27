# Assignment 2 – Set C – Q1: Sorting in Descending Order

## Lab-book task
Explain the modification required to sort integers in descending order with bubble, insertion and selection sort.

## Solution
- **Bubble sort:** change the comparison from `a[j] > a[j+1]` to `a[j] < a[j+1]`, so larger values move toward the front.
- **Insertion sort:** change `temp < a[j]` to `temp > a[j]`.
- **Selection sort:** select the **maximum** element from the unsorted portion instead of the minimum.

The loop structure remains the same.
