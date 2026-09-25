# Assignment 3 – Set B – Q1(b): Employee File by Name using Quick Sort

## Lab-book task
Read employee.txt, sort names alphabetically using strcmp and quick sort, and write sortedemponname.txt.

## Solution
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
typedef struct { char name[100]; int age; float salary; } Employee;
int read_emp(const char*fn,Employee**out){FILE*f=fopen(fn,"r");if(!f){perror(fn);return -1;}Employee*a=NULL,t;int n=0;while(fscanf(f,"%99s %d %f",t.name,&t.age,&t.salary)==3){Employee*p=realloc(a,(n+1)*sizeof(*a));if(!p){free(a);fclose(f);return -1;}a=p;a[n++]=t;}fclose(f);*out=a;return n;}
void write_emp(const char*fn,Employee*a,int n){FILE*f=fopen(fn,"w");if(!f){perror(fn);return;}for(int i=0;i<n;i++)fprintf(f,"%s %d %.2f\n",a[i].name,a[i].age,a[i].salary);fclose(f);}

int partition(Employee*a,int l,int r){Employee pivot=a[l];int i=l,j=r;while(i<j){while(i<j&&strcmp(a[i].name,pivot.name)<=0)i++;while(i<j&&strcmp(a[j].name,pivot.name)>0)j--;if(i<j){Employee t=a[i];a[i]=a[j];a[j]=t;}}a[l]=a[j];a[j]=pivot;return j;}
void quick(Employee*a,int l,int r){if(l<r){int p=partition(a,l,r);quick(a,l,p-1);quick(a,p+1,r);}}
int main(void){Employee*a;int n=read_emp("employee.txt",&a);if(n<0)return 1;quick(a,0,n-1);write_emp("sortedemponname.txt",a,n);for(int i=0;i<n;i++)printf("%s %d %.2f\n",a[i].name,a[i].age,a[i].salary);free(a);return 0;}
```
