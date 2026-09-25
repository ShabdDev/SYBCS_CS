# Assignment 4 – Set C – Q(d): Singly Circular vs Doubly Circular Linked List

## Lab-book task
Explain the difference between singly circular and doubly circular linked lists.

## Solution
- **Singly circular:** each node has `next`; the last node points back to the first. Traversal is normally forward only.
- **Doubly circular:** each node has `next` and `prev`; the last node’s `next` points to the first and the first node’s `prev` points to the last. Traversal is possible in both directions.

Doubly circular lists require more memory per node but support easier predecessor access and deletion of a known node.
