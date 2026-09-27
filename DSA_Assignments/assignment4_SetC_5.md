# Assignment 4 – Set C – Q(e): Reverse Singly Linked List in One Traversal

## Lab-book task
Explain how to reverse a singly linked list in one traversal.

## Solution
Maintain three pointers: `prev`, `current`, and `next`. For each node, save `current->next` in `next`, set `current->next = prev`, then advance `prev = current` and `current = next`. At the end, set `head = prev`. This is O(n) time and O(1) extra space.
