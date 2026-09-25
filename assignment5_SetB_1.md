# Assignment 5 – Set B – Q(a): Stack String Reverse and Palindrome

## Lab-book task
Accept n integers and also reverse a string using a stack and check whether it is a palindrome.

## Solution
```c
#include <stdio.h>
#include <string.h>
#define MAX 200
int main(void){
    int n,st[MAX],top=-1,x; printf("Enter n integers: ");scanf("%d",&n);
    for(int i=0;i<n;i++){scanf("%d",&x);if(top<MAX-1)st[++top]=x;}
    if(top>=0)printf("Popped integer: %d\n",st[top--]);
    char s[MAX],rev[MAX];int ct=-1;printf("Enter string: ");scanf("%199s",s);
    for(int i=0;s[i];i++)st[++ct]=s[i];int i=0;while(ct>=0)rev[i++]=(char)st[ct--];rev[i]='\0';
    printf("Reverse: %s\n",rev);printf("%s\n",strcmp(s,rev)==0?"Palindrome":"Not palindrome");return 0;
}
```
