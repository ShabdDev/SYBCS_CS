# Assignment 5 – Set C – Dynamic Stack Pop Returning the Popped Element

## Lab-book task
Explain how to modify dynamic stack pop so that it returns the changed stack and also gives the popped element to the caller.

## Solution
In C, use an output parameter for the popped value and return the new top pointer:

```c
Node *pop(Node *top, int *value) {
    if (top == NULL) {
        return NULL;
    }
    Node *temp = top;
    *value = temp->data;
    top = temp->next;
    free(temp);
    return top;
}
```

Call it as `top = pop(top, &x);`. This returns the new stack pointer through the function return value and the popped element through `x`.
