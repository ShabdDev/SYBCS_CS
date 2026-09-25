# Assignment 4 – Set B – Q(c): Add Two Single-Variable Polynomials

## Lab-book task
Add two single-variable polynomials represented using linked lists.

## Solution
```c
#include <stdio.h>
#include <stdlib.h>
typedef struct Node{int coef,exp;struct Node*next;}Node;
void insert(Node**h,int c,int e){Node*p=*h,*prev=NULL;while(p&&p->exp>e){prev=p;p=p->next;}if(p&&p->exp==e){p->coef+=c;return;}Node*n=malloc(sizeof*n);n->coef=c;n->exp=e;n->next=p;if(prev)prev->next=n;else *h=n;}
Node* read_poly(void){Node*h=NULL;int n,c,e;printf("Number of terms: ");scanf("%d",&n);for(int i=0;i<n;i++){scanf("%d%d",&c,&e);insert(&h,c,e);}return h;}
Node* add(Node*a,Node*b){Node*r=NULL;while(a){insert(&r,a->coef,a->exp);a=a->next;}while(b){insert(&r,b->coef,b->exp);b=b->next;}return r;}
void print(Node*p){int first=1;while(p){if(p->coef){if(!first&&p->coef>0)printf("+");printf("%dx^%d ",p->coef,p->exp);first=0;}p=p->next;}if(first)printf("0");printf("\n");}
int main(void){printf("P1:\n");Node*a=read_poly();printf("P2:\n");Node*b=read_poly();Node*r=add(a,b);printf("Sum: ");print(r);return 0;}
```
