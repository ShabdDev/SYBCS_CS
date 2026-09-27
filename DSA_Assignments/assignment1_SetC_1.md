# Assignment 1 – Set C – Search Concepts

## Lab-book task
Answer Set C questions on first/last occurrence, best case, comparison counting, and insertion position.

## Solution
### (a) Last occurrence with linear search
Do not stop when the first match is found. Keep a variable such as `last = -1`; whenever `a[i] == x`, set `last = i`. After the loop, `last + 1` is the last 1-based position.

### (b) Binary search: first or last occurrence?
The basic binary-search algorithm in the workbook can return **any one matching occurrence**, depending on where the middle element lands. It does not guarantee the first or last occurrence. To get the first occurrence, record a match and continue searching the left half. To get the last occurrence, record a match and continue searching the right half.

### (c) Best case
For both linear search and binary search, the best case is **O(1)** when the required value is found at the first checked position (for binary search, the initial middle position).

### (d) Count comparisons
For linear search, increment a `comparisons` counter immediately before each `a[i] == x` test. For binary search, increment it before each `a[mid] == x` comparison; if counting every three-way comparison separately, count the equality and ordering tests explicitly. Print the counter after the search.

### (e) Return insertion position
Use a lower-bound style binary search. Maintain `low = 0`, `high = n`; while `low < high`, compute `mid`, and if `a[mid] < x` set `low = mid + 1`, otherwise set `high = mid`. When the loop ends, `low` is the 0-based insertion index that preserves ascending order. If the lab wants a 1-based location, report `low + 1`.
