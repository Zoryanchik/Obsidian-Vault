![[Pasted image 20241123224445.png]]
pointer_to_struct->member
(*pointer_to_struct).member

**Student *ptr = (Student *)malloc(sizeof(Student));**

#include <stdio.h>
#include <stdlib.h>

// Define a structure
typedef struct {
    char name[50];
    int age;
    float marks;
} Student;
int main() {
    // Allocate memory for a Student dynamically
    Student * ptr = (Student * *)malloc(sizeof(Student));

    if (ptr == NULL) {
        printf("Memory allocation failed!\n");
        return 1;
    }

    // Assign values using the -> operator
    printf("Enter name: ");
    scanf("%s", ptr->name);
    printf("Enter age: ");
    scanf("%d", &ptr->age);
    printf("Enter marks: ");
    scanf("%f", &ptr->marks);

    // Access values using the -> operator
    printf("\nStudent Details:\n");
    printf("Name: %s\n", ptr->name);
    printf("Age: %d\n", ptr->age);
    printf("Marks: %.2f\n", ptr->marks);

    // Free allocated memory
    free(ptr);

    return 0;
}


![[Pasted image 20241123231623.png]]![[Pasted image 20241123232222.png]]