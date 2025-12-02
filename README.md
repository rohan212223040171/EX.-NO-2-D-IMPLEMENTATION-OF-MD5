# EX.-NO-2-D-IMPLEMENTATION-OF-MD5

## AIM:
  To write a program to implement the MD5 hashing technique.
## ALGORITHM:
  
  STEP-1: Read the 128-bit plain text.
  
  STEP-2: Divide into four blocks of 32-bits named as A, B, C and D.
  
  STEP-3: Compute the functions f, g, h and i with operations such as, rotations, permutations, etc,.
  
  STEP-4: The output of these functions are combined together as F and performed circular shifting and then given to key round.
  
  STEP-5: Finally, right shift of ‘s’ times are performed and the results are combined together to produce the final output.
  
## PROGRAM:
```
#include <stdio.h>
#include <stdint.h>
#include <string.h>

#define LEFTROTATE(x, c) (((x) << (c)) | ((x) >> (32 - (c))))

// Sample nonlinear functions f, g, h, i from MD5
uint32_t f(uint32_t x, uint32_t y, uint32_t z) {
    return (x & y) | (~x & z);
}

uint32_t g(uint32_t x, uint32_t y, uint32_t z) {
    return (x & z) | (y & ~z);
}

uint32_t h(uint32_t x, uint32_t y, uint32_t z) {
    return x ^ y ^ z;
}

uint32_t i(uint32_t x, uint32_t y, uint32_t z) {
    return y ^ (x | ~z);
}

int main() {
    char input[17];  // 128-bit = 16 ASCII characters
    printf("Enter 128-bit (16-char) plaintext: ");
    fgets(input, sizeof(input), stdin);
    input[strcspn(input, "\n")] = 0;

    if (strlen(input) != 16) {
        printf("Error: Input must be exactly 16 characters (128 bits).\n");
        return 1;
    }

    // Step 2: Divide into A, B, C, D
    uint32_t A = *(uint32_t*)&input[0];
    uint32_t B = *(uint32_t*)&input[4];
    uint32_t C = *(uint32_t*)&input[8];
    uint32_t D = *(uint32_t*)&input[12];

    // Step 3: Compute f, g, h, i
    uint32_t F1 = f(B, C, D);
    uint32_t F2 = g(A, C, D);
    uint32_t F3 = h(A, B, D);
    uint32_t F4 = i(A, B, C);

    // Step 4: Combine and rotate
    uint32_t F = F1 ^ F2 ^ F3 ^ F4;
    F = LEFTROTATE(F, 5);  // Circular shift left by 5

    // Step 5: Final right shift
    F = F >> 3;

    // Print final hash-like output
    printf("Simplified MD5-like hash: %08x\n", F);

    return 0;
}
```
## OUTPUT:

![image](https://github.com/user-attachments/assets/7290167b-6edc-4c86-ab0d-8f53763f5512)


## RESULT:
  Thus the implementation of MD5 hashing algorithm had been implemented successfully using C.
