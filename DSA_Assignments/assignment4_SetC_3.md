# Assignment 4 – Set C – Q(c): More Efficient Operation in Doubly Linked List

## Lab-book task
Identify the operation that is more efficient in a doubly linked list than in a singly linked list.

## Solution
**Deletion of a known node** is more efficient in a doubly linked list because the node has a direct `prev` pointer. In a singly linked list, the predecessor normally has to be found by traversal unless it is already available. The same backward traversal advantage applies to moving to the previous node.
