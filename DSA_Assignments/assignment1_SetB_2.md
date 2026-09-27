# Assignment 1 – Set B – Q1(b): Binary Search in student.txt

## Lab-book task
Read student.txt containing student name and class, accept a name, and use binary search.

## Solution
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct { char name[100]; char class[20]; } Student;

int cmp(const void *a, const void *b) {
    const Student *x = a, *y = b;
    return strcmp(x->name, y->name);
}

int main(void) {
    FILE *fp = fopen("student.txt", "r");
    if (!fp) { perror("student.txt"); return 1; }

    Student *s = NULL;
    size_t n = 0;
    Student temp;
    while (fscanf(fp, "%99s %19s", temp.name, temp.class) == 2) {
        Student *p = realloc(s, (n + 1) * sizeof(*s));
        if (!p) { free(s); fclose(fp); return 1; }
        s = p; s[n++] = temp;
    }
    fclose(fp);

    qsort(s, n, sizeof(*s), cmp); /* binary search needs sorted data */

    char target[100];
    printf("Enter student name: ");
    scanf("%99s", target);

    size_t low = 0, high = n;
    int found = 0;
    while (low < high) {
        size_t mid = low + (high - low) / 2;
        int c = strcmp(target, s[mid].name);
        if (c == 0) {
            printf("Class of %s: %s\n", s[mid].name, s[mid].class);
            found = 1; break;
        }
        if (c < 0) high = mid;
        else low = mid + 1;
    }
    if (!found) printf("Student not in the list.\n");
    free(s);
    return 0;
}
```

## Notes / assumptions
The workbook states the file contains names and classes. This solution sorts the records in memory first so the binary-search precondition is guaranteed.
