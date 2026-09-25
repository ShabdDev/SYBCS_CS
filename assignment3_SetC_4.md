# Assignment 3 – Set C – Q4: Equal Names in Merge Sort vs Quick Sort

## Lab-book task
Explain the relative ordering of records having the same name when sorted by name.

## Solution
A merge-sort implementation that chooses the left element when keys are equal (`<=`) is **stable**, so records with equal names retain their original relative order. The workbook’s quick-sort partition does not guarantee stability; equal-name records may change relative order. Stability therefore depends on the exact implementation, but ordinary in-place quick sort is not stable.
