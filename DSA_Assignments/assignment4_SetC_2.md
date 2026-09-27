# Assignment 4 – Set C – Q(b): O(1) Union of Disjoint Sets

## Lab-book task
Explain how to implement union of two disjoint sets in O(1) time using a suitable list representation.

## Solution
Represent each set by a linked list with both **head and tail pointers**. To union disjoint sets `S1` and `S2`, connect `S1.tail->next = S2.head`, set the new tail to `S2.tail`, and discard the separate S2 descriptor. The pointer operations are O(1). This assumes the sets are disjoint as stated and that the representation maintains a tail pointer.
