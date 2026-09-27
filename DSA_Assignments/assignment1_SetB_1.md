# Assignment 1 – Set B – Q1(a): Linear Search in student.txt

## Lab-book task
Read student.txt containing student name and class (FY/SY/TY), accept a student name, and use linear search.

## Solution
```c
#include <stdio.h>
#include <string.h>

int main(void) {
    FILE *fp = fopen("student.txt", "r");
    if (!fp) { perror("student.txt"); return 1; }

    char target[100], name[100], class[20];
    int found = 0;
    printf("Enter student name: ");
    scanf("%99s", target);

    while (fscanf(fp, "%99s %19s", name, class) == 2) {
        if (strcmp(name, target) == 0) {
            printf("Class of %s: %s\n", name, class);
            found = 1;
            break;
        }
    }
    if (!found) printf("Student not in the list.\n");
    fclose(fp);
    return 0;
}
```

## Notes / assumptions
Expected file format: one record per line, e.g. `Amit FY`. Names are treated as single tokens.
