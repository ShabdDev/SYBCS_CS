# Assignment 6 – Set B – Q(a): Circular Queue

## Lab-book task
Create a circular queue of n integers and delete/display the front element.

## Solution
```c
#include <stdio.h>
#define MAX 100
int q[MAX],front=-1,rear=-1;
int isEmpty(void){return front==-1;}
int isFull(void){return (rear==MAX-1&&front==0)||(rear+1==front);}
void add(int x){if(isFull()){printf("Queue is full\n");return;}if(front==-1)front=rear=0;else rear=(rear+1)%MAX;q[rear]=x;}
int del(void){if(isEmpty())return 0;int x=q[front];if(front==rear)front=rear=-1;else front=(front+1)%MAX;return x;}
int main(void){int n,x;printf("Enter n: ");scanf("%d",&n);for(int i=0;i<n;i++){scanf("%d",&x);add(x);}if(!isEmpty())printf("Deleted: %d\n",del());else printf("Queue is empty\n");return 0;}
```
