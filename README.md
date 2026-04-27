# EX. NO: 3 IMPLEMENTATION OF HILL CIPHER

## AIM:

To write a C program to implement the hill cipher substitution techniques.

## DESCRIPTION:

Each letter is represented by a number modulo 26. Often the simple scheme A = 0, B = 1... Z = 25 is used, but this is not an essential feature of the cipher. 

To encrypt a message, each block of n letters is  multiplied by an invertible n × n matrix, against modulus 26. 

To decrypt the message, each block is multiplied by the inverse of the m trix used for encryption.

The matrix used for encryption is the cipher key, and it shold be chosen randomly from the set of invertible n × n matrices (modulo 26).

## ALGORITHM:

STEP-1: Read the plain text and key from the user.

STEP-2: Split the plain text into groups of length three.

STEP-3: Arrange the keyword in a 3*3 matrix.

STEP-4: Multiply the two matrices to obtain the cipher text of length three.

STEP-5: Combine all these groups to get the complete cipher text.

## PROGRAM

```
#include <stdio.h>
#include <string.h>
#include <ctype.h>

int keymat[3][3] = { { 1, 2, 1 }, { 2, 3, 2 }, { 2, 2, 1 } };
int invkeymat[3][3] = { { -1, 0, 1 }, { 2, -1, 0 }, { -2, 2, -1 } };
char key[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

void encode(char a, char b, char c, char ret[4]) 
{
    int x, y, z;
    int posa = (int)a - 65;
    int posb = (int)b - 65;
    int posc = (int)c - 65;
    x = posa * keymat[0][0] + posb * keymat[1][0] + posc * keymat[2][0];
    y = posa * keymat[0][1] + posb * keymat[1][1] + posc * keymat[2][1];
    z = posa * keymat[0][2] + posb * keymat[1][2] + posc * keymat[2][2];
    ret[0] = key[(x % 26 + 26) % 26];
    ret[1] = key[(y % 26 + 26) % 26];
    ret[2] = key[(z % 26 + 26) % 26];
    ret[3] = '\0';
}

void decode(char a, char b, char c, char ret[4]) 
{
    int x, y, z;
    int posa = (int)a - 65;
    int posb = (int)b - 65;
    int posc = (int)c - 65;
    x = posa * invkeymat[0][0] + posb * invkeymat[1][0] + posc * invkeymat[2][0];
    y = posa * invkeymat[0][1] + posb * invkeymat[1][1] + posc * invkeymat[2][1];
    z = posa * invkeymat[0][2] + posb * invkeymat[1][2] + posc * invkeymat[2][2];
    ret[0] = key[(x % 26 + 26) % 26];
    ret[1] = key[(y % 26 + 26) % 26];
    ret[2] = key[(z % 26 + 26) % 26];
    ret[3] = '\0';
}

int main() 
{
    char msg[1000];
    char enc[1000] = "";
    char dec[1000] = "";
    int n;
    printf("Enter plain text: ");
    scanf("%s", msg);
    printf("\nSimulation of Hill Cipher\n");
    printf("\nInput message : %s\n", msg);
    for (int i = 0; i < strlen(msg); i++) 
    {
        msg[i] = toupper(msg[i]);
    }
    n = strlen(msg) % 3;
    if (n != 0) 
    {
        for (int i = 1; i <= (3 - n); i++) 
        {
            strcat(msg, "X");
        }
    }
    printf("\nPadded message : %s\n", msg);
    for (int i = 0; i < strlen(msg); i += 3) 
    {
        char ret[4];
        encode(msg[i], msg[i+1], msg[i+2], ret);
        strcat(enc, ret);
    }
    printf("\nEncoded message : %s\n", enc);
    for (int i = 0; i < strlen(enc); i += 3) 
    {
        char ret[4];
        decode(enc[i], enc[i+1], enc[i+2], ret);
        strcat(dec, ret);
    }
    printf("\nDecoded message : %s\n", dec);
    return 0;
}
```

## OUTPUT

<img width="1910" height="937" alt="ex3op" src="https://github.com/user-attachments/assets/caf62b41-726c-4b89-a306-b71972d1e20e" />

## RESULT
Thus, the implementation of Hill Cipher had been executed successfully.
