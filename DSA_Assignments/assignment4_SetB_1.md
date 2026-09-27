# Assignment 4 – Set B – Library: doublylist.h + Insert/Search/Delete

## Lab-book task
Implement a doubly linked-list library and a menu-driven program for insert, search, and delete.

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

#include "doublylist.h"
int main(void){DNode*h=NULL;int ch,x,pos;while(1){printf("1.Insert 2.Search 3.Delete 4.Display 5.Exit: ");scanf("%d",&ch);if(ch==1){scanf("%d%d",&x,&pos);dinsert(&h,x,pos);}else if(ch==2){scanf("%d",&x);printf(dsearch(h,x)?"Found\n":"Not found\n");}else if(ch==3){scanf("%d",&x);ddelete(&h,x);}else if(ch==4)ddisplay(h);else break;}return 0;}
```

## Notes / assumptions
Save the library portion as `doublylist.h` and the main program as a separate `.c` file.
