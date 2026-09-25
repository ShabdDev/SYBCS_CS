# Assignment 6 – Set C – Railway Reservation Waiting List

## Lab-book task
Implement a queue library and use it to simulate railway reservation waiting-list operations.

## Solution
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
typedef struct Node{int token;char name[50];struct Node*next;}Node;
Node*front=NULL,*rear=NULL;int next_token=1;
void enqueue(const char*name){Node*n=malloc(sizeof*n);n->token=next_token++;strncpy(n->name,name,49);n->name[49]='\0';n->next=NULL;if(!rear)front=rear=n;else{rear->next=n;rear=n;}printf("Waiting-list token: %d\n",n->token);}
void dequeue(void){if(!front){printf("Waiting list empty\n");return;}Node*n=front;printf("Confirmed passenger: %d %s\n",n->token,n->name);front=front->next;if(!front)rear=NULL;free(n);}
void display(void){for(Node*p=front;p;p=p->next)printf("%d %s\n",p->token,p->name);}
int main(void){int ch;char name[50];while(1){printf("1.Add passenger 2.Confirm first 3.Display waiting list 4.Exit: ");scanf("%d",&ch);if(ch==1){printf("Name: ");scanf("%49s",name);enqueue(name);}else if(ch==2)dequeue();else if(ch==3)display();else break;}return 0;}
```

## Notes / assumptions
The queue preserves FIFO order, which models a basic waiting list. A real reservation system would need additional business rules such as cancellation, priority categories, and persistence.
