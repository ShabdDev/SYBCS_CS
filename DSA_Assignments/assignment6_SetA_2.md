# Assignment 6 – Set A – Q1(b): Dynamic Linear Queue

## Lab-book task
Insert n elements into a dynamically implemented queue, delete the front element, and display it.

## Solution
```c
#include <stdio.h>
#include <stdlib.h>
typedef struct Node{int data;struct Node*next;}Node;
Node *front=NULL,*rear=NULL;
void add(int x){Node*n=malloc(sizeof*n);if(!n)exit(1);n->data=x;n->next=NULL;if(!rear)front=rear=n;else{rear->next=n;rear=n;}}
int isEmpty(void){return front==NULL;}
int deleteq(void){int x=front->data;Node*n=front;front=front->next;if(!front)rear=NULL;free(n);return x;}
int main(void){int n,x;printf("Enter n: ");scanf("%d",&n);for(int i=0;i<n;i++){scanf("%d",&x);add(x);}if(!isEmpty())printf("Deleted element: %d\n",deleteq());else printf("Queue is empty\n");return 0;}
```
