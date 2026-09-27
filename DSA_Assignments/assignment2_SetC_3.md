# Assignment 2 – Set C – Q3: Count Insertion-Sort Key Comparisons

## Lab-book task
Explain the modification required to count key comparisons in insertion sort.

## Solution
Initialize `comparisons = 0`. Each time the condition comparing `temp` with `a[j]` is evaluated, increment the counter. If you want to count only key-to-key comparisons, count `temp > a[j]`/`temp < a[j]` and treat the `j >= 0` boundary check separately. A robust loop is:

`while (j >= 0) { comparisons++; if (temp >= a[j]) break; a[j+1] = a[j]; j--; }`
