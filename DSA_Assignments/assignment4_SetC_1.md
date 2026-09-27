# Assignment 4 – Set C – Q(a): Split Singly Linked List into Two Almost Equal Lists

## Lab-book task
Explain and implement the split of a singly linked list into two almost equal-sized lists.

## Solution
Use the **slow/fast pointer** technique. Start `slow=head`, `fast=head->next`. Move `slow` one node and `fast` two nodes until `fast` cannot move two nodes. Then the second list starts at `slow->next`; set `slow->next = NULL`. For an odd number of nodes, the first list receives one extra node. This takes O(n) time and O(1) extra pointer space.
