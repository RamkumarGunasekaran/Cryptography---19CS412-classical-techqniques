## NAME: RAMKUMAR G
## REG NO: 212223220084

# Cryptography---19CS412-classical-techniques
# Caeser Cipher
Caeser Cipher using with different key values
# AIM:
To encrypt and decrypt the given message by using Ceaser Cipher encryption algorithm.
# DESIGN STEPS:
## Step 1:
Design of Caeser Cipher algorithnm
## Step 2:
Design of Caeser Cipher algorithnm
## Step 3:
1. In Ceaser Cipher each letter in the plaintext is replaced by a letter some fixed number of positions down the alphabet.
2. For example, with a left shift of 3, D would be replaced by A, E would become B, and so on.
3. The encryption can also be represented using modular arithmetic by first transforming the letters into numbers, according to the
scheme, A = 0, B = 1, Z = 25.
4. Encryption of a letter x by a shift n can be described mathematically as, En(x) = (x + n) mod26
5. Decryption is performed similarly, Dn (x)=(x - n) mod26
# PROGRAM
```
PROGRAM 01;
#include <stdio.h>
#include <string.h>
#include <conio.h>
#include <ctype.h>
void main()

{
    char plain[10],cipher[10];
    int key,i,length;
    int result;
    printf("\n Enter the plain text:");
    scanf("%s", plain);
    printf("\n Enter the key value:");
    scanf("%d", &key);
    printf("\n \n \t PLAIN TEXt: %s", plain);
    printf("\n \n \t ENCRYPTED TEXT:");
    for(i=0, length = strlen(plain); i<length; i++)
    {
        
        cipher[i]=plain[i] + key;
        if (isupper(plain[i]) && (cipher[i] > 'Z'))
        cipher[i] = cipher[i] - 26;
        if (islower(plain[i]) && (cipher[i] > 'z'))
        cipher[i] = cipher[i] - 26;
        printf("%c", cipher[i]);

    }
    printf("\n \n \t AFTER DECRYPTION : ");
    for(i=0;i<length;i++)
    {
        
        plain[i]=cipher[i]-key;
        if(isupper(cipher[i])&&(plain[i]<'A'))
        plain[i]=plain[i]+26;
        if(islower(cipher[i])&&(plain[i]<'a'))
        plain[i]=plain[i]+26;
        printf("%c",plain[i]);
    }
    getch();

    
}

```
# OUTPUT
![Screenshot 2025-03-19 092418](https://github.com/user-attachments/assets/4a873196-c249-409a-a9f2-72d31ae91ec3)

# RESULT:
The program is executed successfully.




