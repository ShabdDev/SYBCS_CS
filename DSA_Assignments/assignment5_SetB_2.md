# Assignment 5 – Set B – Q(b): Infix to Postfix and Postfix Evaluation

## Lab-book task
Convert `(a*(b-c*d)/((a+d)/b))` to postfix and provide a menu-driven implementation for conversion/evaluation.

## Solution
```c
#include <stdio.h>
#include <ctype.h>
#include <string.h>
#include <stdlib.h>
#define MAX 200
int prec(char c){if(c=='^'||c=='$')return 3;if(c=='*'||c=='/'||c=='%')return 2;if(c=='+'||c=='-')return 1;return 0;}
void infix_to_postfix(const char*in,char*out){char st[MAX];int top=-1,k=0;for(int i=0;in[i];i++){char c=in[i];if(isalnum((unsigned char)c))out[k++]=c;else if(c=='(')st[++top]=c;else if(c==')'){while(top>=0&&st[top]!='(')out[k++]=st[top--];if(top>=0)top--;}else{while(top>=0&&st[top]!='('&&prec(st[top])>=prec(c))out[k++]=st[top--];st[++top]=c;}}while(top>=0)out[k++]=st[top--];out[k]='\0';}
int eval_postfix(const char*e){int st[MAX],top=-1;for(int i=0;e[i];i++){char c=e[i];if(isdigit((unsigned char)c))st[++top]=c-'0';else{if(top<1){printf("Invalid postfix expression\n");return 0;}int b=st[top--],a=st[top--];switch(c){case '+':st[++top]=a+b;break;case '-':st[++top]=a-b;break;case '*':st[++top]=a*b;break;case '/':st[++top]=a/b;break;case '%':st[++top]=a%b;break;default:return 0;}}}return st[top];}
int main(void){char in[MAX],post[MAX];int ch;while(1){printf("1.Infix to postfix 2.Evaluate numeric postfix 3.Exit: ");scanf("%d",&ch);if(ch==1){printf("Enter infix: ");scanf("%199s",in);infix_to_postfix(in,post);printf("Postfix: %s\n",post);}else if(ch==2){printf("Enter numeric postfix (single digits): ");scanf("%199s",post);printf("Result: %d\n",eval_postfix(post));}else break;}return 0;}
```

## Notes / assumptions
For the exact workbook expression, the postfix form is `abcd*-*ad+b//`. Numeric postfix evaluation in this program supports single-digit operands.
