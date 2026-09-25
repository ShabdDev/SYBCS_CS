# Assignment 4 – Set A – Q1(a): Singly Linked List Insert/Search/Delete

## Lab-book task
Menu-driven singly linked list: insert at position, search, and delete a particular element.

## Solution
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct Node { int data; struct Node *next; } Node;
Node *head=NULL;
Node* new_node(int x){Node*n=malloc(sizeof(*n));if(!n){perror("malloc");exit(1);}n->data=x;n->next=NULL;return n;}
void display(void){for(Node*p=head;p;p=p->next)printf("%d -> ",p->data);printf("NULL\n");}
void insert_pos(int x,int pos){Node*n=new_node(x);if(pos<=1||!head){n->next=head;head=n;return;}Node*p=head;for(int i=1;i<pos-1&&p->next;i++)p=p->next;n->next=p->next;p->next=n;}
int search(int x){int pos=1;for(Node*p=head;p;p=p->next,pos++)if(p->data==x)return pos;return -1;}
void delete_value(int x){Node*p=head,*prev=NULL;while(p&&p->data!=x){prev=p;p=p->next;}if(!p){printf("Element not found.\n");return;}if(prev)prev->next=p->next;else head=p->next;free(p);}
void reverse(void){Node*prev=NULL,*cur=head;while(cur){Node*n=cur->next;cur->next=prev;prev=cur;cur=n;}head=prev;}
void append(int x){Node*n=new_node(x);if(!head){head=n;return;}Node*p=head;while(p->next)p=p->next;p->next=n;}
Node* merge_lists(Node*a,Node*b){if(!a)return b;Node*p=a;while(p->next)p=p->next;p->next=b;return a;}
void free_list(void){while(head){Node*n=head->next;free(head);head=n;}}
int main(void){int ch,x,pos;while(1){printf("\n1.Insert 2.Search 3.Delete 4.Display 5.Reverse 6.Append 7.Exit\nChoice: ");scanf("%d",&ch);switch(ch){case 1:printf("Value position: ");scanf("%d%d",&x,&pos);insert_pos(x,pos);break;case 2:printf("Value: ");scanf("%d",&x);pos=search(x);if(pos==-1)printf("Not found\n");else printf("Found at position %d\n",pos);break;case 3:printf("Value: ");scanf("%d",&x);delete_value(x);break;case 4:display();break;case 5:reverse();display();break;case 6:printf("Value: ");scanf("%d",&x);append(x);display();break;case 7:free_list();return 0;default:printf("Invalid choice\n");}}}
```
