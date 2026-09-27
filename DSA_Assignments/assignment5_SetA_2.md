# Assignment 5 – Set A – Q1(b): Dynamic Stack

## Lab-book task
Accept n integers into a dynamically implemented stack, pop and display an element.

## Solution
```c
#include <stdio.h>
#include <stdlib.h>
typedef struct Node{int data;struct Node*next;}Node;
Node*top=NULL;
void push(int x){Node*n=malloc(sizeof*n);if(!n)exit(1);n->data=x;n->next=top;top=n;}
int isEmpty(void){return top==NULL;}
int pop(void){int x=top->data;Node*n=top;top=top->next;free(n);return x;}
int main(void){int n,x;printf("Enter n: ");scanf("%d",&n);for(int i=0;i<n;i++){scanf("%d",&x);push(x);}if(!isEmpty())printf("Popped element: %d\n",pop());else printf("Stack is empty\n");return 0;}
```
