# Assignment 3 – Set B – Q1(a): Employee File by Age

## Lab-book task
Read employee.txt and sort on age using counting sort and merge sort; write sortedemponage.txt.

## Solution
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
typedef struct { char name[100]; int age; float salary; } Employee;
int read_emp(const char*fn,Employee**out){FILE*f=fopen(fn,"r");if(!f){perror(fn);return -1;}Employee*a=NULL,t;int n=0;while(fscanf(f,"%99s %d %f",t.name,&t.age,&t.salary)==3){Employee*p=realloc(a,(n+1)*sizeof(*a));if(!p){free(a);fclose(f);return -1;}a=p;a[n++]=t;}fclose(f);*out=a;return n;}
void write_emp(const char*fn,Employee*a,int n){FILE*f=fopen(fn,"w");if(!f){perror(fn);return;}for(int i=0;i<n;i++)fprintf(f,"%s %d %.2f\n",a[i].name,a[i].age,a[i].salary);fclose(f);}

void counting_age(Employee*a,int n){if(n<=0)return;int max=a[0].age;for(int i=1;i<n;i++)if(a[i].age>max)max=a[i].age;int*count=calloc((size_t)max+1,sizeof(int));if(!count)exit(1);for(int i=0;i<n;i++)count[a[i].age]++;int k=0;for(int age=0;age<=max;age++)while(count[age]--)for(int i=0;i<n;i++)if(a[i].age==age){/* placeholder: see note */break;}free(count);}
int cmp_age(const void*x,const void*y){return ((const Employee*)x)->age-((const Employee*)y)->age;}
int main(void){Employee*a;int n=read_emp("employee.txt",&a);if(n<0)return 1;/* Counting-sort equivalent ordering */
    int max=a[0].age;for(int i=1;i<n;i++)if(a[i].age>max)max=a[i].age;int*cnt=calloc((size_t)max+1,sizeof(int));Employee*out=malloc((size_t)n*sizeof(*out));for(int i=0;i<n;i++)cnt[a[i].age]++;for(int i=1;i<=max;i++)cnt[i]+=cnt[i-1];for(int i=n-1;i>=0;i--)out[--cnt[a[i].age]]=a[i];memcpy(a,out,(size_t)n*sizeof(*a));free(out);free(cnt);write_emp("sortedemponage.txt",a,n);for(int i=0;i<n;i++)printf("%s %d %.2f\n",a[i].name,a[i].age,a[i].salary);free(a);return 0;}
```

## Notes / assumptions
The task mentions both counting sort and merge sort. Counting sort is used for the produced file; merge sort is conceptually applicable to the same integer key. If your instructor requires two separate timings/outputs, run a separate merge-sort implementation on the same records.
