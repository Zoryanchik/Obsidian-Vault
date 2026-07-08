![[Pasted image 20241123223354.png]]
Int,charn,string ext
![[Pasted image 20241123223451.png]]
struct structure_name {
    data_type field1;
    data_type field2;
    ...
};

**Typedef**
#include <stdio.h>

typedef unsigned int uint; // Alias for unsigned int

int main() {
    uint age = 25; // uint is now a synonym for unsigned int
    printf("Age: %u\n", age);
    return 0;
}

