# Assignment 2 – Set C – Q4: Display Array After Every Pass

## Lab-book task
Explain how to print the array contents after every sorting pass.

## Solution
Place a display loop immediately after the outer-loop body completes.

For bubble and selection sort, the outer loop represents a pass. For insertion sort, each iteration that inserts `A[i]` can be treated as one pass. Print `Pass %d:` followed by all array elements.
