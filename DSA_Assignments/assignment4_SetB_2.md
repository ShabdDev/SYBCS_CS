# Assignment 4 – Set B – Q(b): Doubly Linked List Reverse/Concatenate/Merge

## Lab-book task
Menu-driven program for reversing, appending and merging doubly linked lists.

## Solution
```c
#ifndef DOUBLYLIST_H
#define DOUBLYLIST_H
#include <stdio.h>
#include <stdlib.h>
typedef struct DNode{int data;struct DNode*prev,*next;}DNode;
static DNode*dnew(int x){DNode*n=malloc(sizeof* n);n->data=x;n->prev=n->next=NULL;return n;}
static void dappend(DNode**h,int x){DNode*n=dnew(x);if(!*h){*h=n;return;}DNode*p=*h;while(p->next)p=p->next;p->next=n;n->prev=p;}
static void dinsert(DNode**h,int x,int pos){DNode*n=dnew(x);if(pos<=1||!*h){n->next=*h;if(*h)(*h)->prev=n;*h=n;return;}DNode*p=*h;for(int i=1;i<pos-1&&p->next;i++)p=p->next;n->next=p->next;n->prev=p;if(p->next)p->next->prev=n;p->next=n;}
static DNode*dsearch(DNode*h,int x){for(;h;h=h->next)if(h->data==x)return h;return NULL;}
static void ddelete(DNode**h,int x){DNode*p=dsearch(*h,x);if(!p)return;if(p->prev)p->prev->next=p->next;else *h=p->next;if(p->next)p->next->prev=p->prev;free(p);}
static void ddisplay(DNode*h){for(;h;h=h->next)printf("%d <-> ",h->data);printf("NULL\n");}
#endif

void reverse(DNode**h){DNode*p=*h,*tmp=NULL;while(p){tmp=p->prev;p->prev=p->next;p->next=tmp;if(!p->prev)*h=p;p=p->prev;}}
DNode* merge(DNode*a,DNode*b){if(!a)return b;DNode*p=a;while(p->next)p=p->next;p->next=b;if(b)b->prev=p;return a;}
int main(void){DNode*a=NULL,*b=NULL;int n,x,ch;printf("n for A: ");scanf("%d",&n);for(int i=0;i<n;i++){scanf("%d",&x);dappend(&a,x);}while(1){printf("1.Reverse 2.Append 3.Merge B 4.Display 5.Exit: ");scanf("%d",&ch);if(ch==1)reverse(&a);else if(ch==2){scanf("%d",&x);dappend(&a,x);}else if(ch==3){printf("n for B: ");scanf("%d",&n);for(int i=0;i<n;i++){scanf("%d",&x);dappend(&b,x);}a=merge(a,b);b=NULL;}else if(ch==4)ddisplay(a);else break;}return 0;}
```
