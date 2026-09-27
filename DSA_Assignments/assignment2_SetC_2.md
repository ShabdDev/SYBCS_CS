# Assignment 2 – Set C – Q2: Count Bubble-Sort Swaps

## Lab-book task
Explain the modification required to count swaps in bubble sort.

## Solution
Initialize `swaps = 0` before sorting. Inside the exchange block, increment it after every swap:

`if (a[j] > a[j+1]) { swap(a[j], a[j+1]); swaps++; }`

Print `swaps` after sorting. With an early-exit optimization, a sorted input can finish with zero swaps.
