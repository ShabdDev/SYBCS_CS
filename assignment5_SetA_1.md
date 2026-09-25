# Assignment 5 – Set A – Q1(a): Static Stack

## Lab-book task
Accept n integers into a static stack, then pop and display an element using isEmpty().

## Solution
```c
#include <stdio.h>
#define MAX 100
int stack[MAX], top=-1;
int isEmpty(void){return top==-1;}
int isFull(void){return top==MAX-1;}
void push(int x){if(isFull()){printf("Stack overflow\n");return;}stack[++top]=x;}
int pop(void){return stack[top--];}
int main(void){int n,x;printf("Enter n (<=%d): ",MAX);scanf("%d",&n);for(int i=0;i<n;i++){scanf("%d",&x);push(x);}if(!isEmpty())printf("Popped element: %d\n",pop());else printf("Stack is empty\n");return 0;}
```
