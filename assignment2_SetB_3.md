# Assignment 2 – Set B – Q1(c): Selection Sort Student.txt by Percentage

## Lab-book task
Read Student.txt, sort by Percentage using selection sort, and create a separate sorted file.

## Solution
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct { char name[100]; int age; float percentage; } Student;

int read_students(const char *file, Student **out) {
    FILE *fp=fopen(file,"r"); if(!fp){perror(file);return -1;}
    Student *a=NULL,t; int n=0;
    while(fscanf(fp,"%99s %d %f",t.name,&t.age,&t.percentage)==3){
        Student *p=realloc(a,(n+1)*sizeof(*a)); if(!p){free(a);fclose(fp);return -1;}
        a=p; a[n++]=t;
    }
    fclose(fp); *out=a; return n;
}
void write_students(const char *file, Student *a, int n){
    FILE *fp=fopen(file,"w"); if(!fp){perror(file);return;}
    for(int i=0;i<n;i++) fprintf(fp,"%s %d %.2f\n",a[i].name,a[i].age,a[i].percentage);
    fclose(fp);
}
void print_students(Student *a,int n){for(int i=0;i<n;i++)printf("%s %d %.2f\n",a[i].name,a[i].age,a[i].percentage);}

int main(void){
    Student *a; int n=read_students("Student.txt",&a); if(n<0)return 1;
    for(int i=0;i<n-1;i++){int min=i;for(int j=i+1;j<n;j++)if(a[j].percentage<a[min].percentage)min=j;if(min!=i){Student t=a[i];a[i]=a[min];a[min]=t;}}
    write_students("sorted_student_by_percentage.txt",a,n); print_students(a,n); free(a); return 0;
}
```
