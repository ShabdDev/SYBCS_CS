# Assignment 6 – Set B – Q(b): Priority Queue

## Lab-book task
Create a priority queue, insert elements with priorities, and delete according to priority.

## Solution
```c
#include <stdio.h>
#define MAX 100
typedef struct{int data,priority,order;}Item;Item q[MAX];int n=0;
void add(int x,int p){if(n==MAX){printf("Full\n");return;}q[n++]=(Item){x,p,n};}
int delete_highest(void){if(!n)return -1;int k=0;for(int i=1;i<n;i++)if(q[i].priority>q[k].priority)k=i;int x=q[k].data;for(int i=k;i<n-1;i++)q[i]=q[i+1];n--;return x;}
int main(void){int ch,x,p;while(1){printf("1.Add 2.Delete highest priority 3.Display 4.Exit: ");scanf("%d",&ch);if(ch==1){printf("Element priority: ");scanf("%d%d",&x,&p);add(x,p);}else if(ch==2){x=delete_highest();if(x==-1)printf("Empty\n");else printf("Deleted: %d\n",x);}else if(ch==3){for(int i=0;i<n;i++)printf("%d(p%d) ",q[i].data,q[i].priority);printf("\n");}else break;}return 0;}
```

## Notes / assumptions
Higher numeric priority is treated as higher priority. Equal priorities remain first-come-first-served because the scan only replaces the selected item when a strictly higher priority is found.
