# Assignment 3 – Set C – Q5: Sorted Input and Sorting Time

## Lab-book task
Explain how to compare quick-sort and merge-sort time on random versus already-sorted files.

## Solution
Generate a large random array and save it. Create its sorted version. Time quick sort on the random file and sorted file, then repeat with merge sort. A quick sort that always selects the first element can degrade badly on already-sorted data, approaching O(n²). A merge sort remains O(n log n) regardless of whether the input is already sorted. Therefore, a sorted file does **not** universally give the best time; it depends on the algorithm and implementation.
