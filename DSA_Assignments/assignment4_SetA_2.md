# Assignment 4 – Set A – Q1(b): Singly Linked List Reverse/Concatenate/Merge

## Lab-book task
Menu-driven singly linked list operations for reverse, concatenate/append, and merge.

## Solution
```c
#include <stdio.h>
#include <stdlib.h>
typedef struct Node{int data;struct Node*next;}Node;
Node* node(int x){Node*n=malloc(sizeof* n);n->data=x;n->next=NULL;return n;}
void append(Node**h,int x){Node*n=node(x);if(!*h){*h=n;return;}Node*p=*h;while(p->next)p=p->next;p->next=n;}
void display(Node*h){while(h){printf("%d -> ",h->data);h=h->next;}printf("NULL\n");}
void reverse(Node**h){Node*p=NULL,*c=*h;while(c){Node*n=c->next;c->next=p;p=c;c=n;}*h=p;}
Node* merge(Node*a,Node*b){if(!a)return b;Node*p=a;while(p->next)p=p->next;p->next=b;return a;}
void free_list(Node*h){while(h){Node*n=h->next;free(h);h=n;}}
int main(void){Node*a=NULL,*b=NULL;int n,x,ch;printf("Enter number of elements in list A: ");scanf("%d",&n);for(int i=0;i<n;i++){scanf("%d",&x);append(&a,x);}printf("A: ");display(a);while(1){printf("1.Reverse A 2.Append to A 3.Create B and merge 4.Exit: ");scanf("%d",&ch);if(ch==1){reverse(&a);display(a);}else if(ch==2){printf("Element: ");scanf("%d",&x);append(&a,x);display(a);}else if(ch==3){printf("Number of B elements: ");scanf("%d",&n);b=NULL;for(int i=0;i<n;i++){scanf("%d",&x);append(&b,x);}a=merge(a,b);b=NULL;display(a);}else break;}free_list(a);return 0;}
```

## Notes / assumptions
“Concatenate” is implemented as appending an element to the created list, matching the wording of the workbook task.
