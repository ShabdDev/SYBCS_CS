# Assignment 6 – Set A – Q1(a): Static Linear Queue

## Lab-book task
Create a static queue of n integers, delete the front element, and display it.

## Solution
```c
#include <stdio.h>
#define MAX 100
int q[MAX],front=-1,rear=-1;
int isEmpty(void){return front==-1 || front>rear;}
int isFull(void){return rear==MAX-1;}
void add(int x){if(isFull()){printf("Queue full\n");return;}if(front==-1)front=0;q[++rear]=x;}
int deleteq(void){int x=q[front++];if(front>rear)front=rear=-1;return x;}
int main(void){int n,x;printf("Enter n: ");scanf("%d",&n);for(int i=0;i<n;i++){scanf("%d",&x);add(x);}if(!isEmpty())printf("Deleted element: %d\n",deleteq());else printf("Queue is empty\n");return 0;}
```
