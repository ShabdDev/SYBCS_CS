# Assignment 3 – Set C – Q2: Compare Merge Sort and Bubble Sort Time

## Lab-book task
Use the Linux `time` command to compare sorting time on a random array of at least 10000 integers.

## Solution
Create two programs that generate the same-size random input, one using bubble sort and one using merge sort. Compile them with optimization disabled or consistently enabled, then run:

```text
/usr/bin/time -f "Elapsed: %e s" ./bubble
/usr/bin/time -f "Elapsed: %e s" ./merge
```

Use the same input size and comparable workload. Bubble sort performs quadratically in the average/worst case, while merge sort runs in O(n log n), so the measured times should be interpreted together with the algorithmic complexity rather than as a universal benchmark.
