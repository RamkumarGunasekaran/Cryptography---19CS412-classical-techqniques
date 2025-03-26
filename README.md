## NAME: RAMKUMAR G
## REG NO: 212223220084


# Cryptography---19CS412-classical-techniques
# Caeser Cipher
Caeser Cipher using with different key values
# AIM:
To encrypt and decrypt the given message by using Ceaser Cipher encryption algorithm.
## DESIGN STEPS:
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
## PROGRAM
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
## OUTPUT
![Screenshot 2025-03-19 092418](https://github.com/user-attachments/assets/4a873196-c249-409a-a9f2-72d31ae91ec3)

## RESULT:
The program is executed successfully.



## NAME: RAMKUMAR G
## REG NO: 212223220084


# PlayFair Cipher
Playfair Cipher using with different key values

# AIM:
To implement a program to encrypt a plain text and decrypt a cipher text using play fair Cipher substitution technique.

## DESIGN STEPS:
## Step 1:
Design of PlayFair Cipher algorithnm

## Step 2:
Implementation using C or pyhton code

## Step 3:
Testing algorithm with different key values.

ALGORITHM DESCRIPTION: The Playfair cipher uses a 5 by 5 table containing a key word or phrase. To generate the key table, first fill the spaces in the table with the letters of the keyword, then fill the remaining spaces with the rest of the letters of the alphabet in order (usually omitting "Q" to reduce the alphabet to fit; other versions put both "I" and "J" in the same space). The key can be written in the top rows of the table, from left to right, or in some other pattern, such as a spiral beginning in the upper-left-hand corner and ending in the centre. The keyword together with the conventions for filling in the 5 by 5 table constitutes the cipher key. To encrypt a message, one would break the message into digrams (groups of 2 letters) such that, for example, "HelloWorld" becomes "HE LL OW OR LD", and map them out on the key table. Then apply the following 4 rules, to each pair of letters in the plaintext:

1.If both letters are the same (or only one letter is left), add an "X" after the first letter. Encrypt the new pair and continue. Some
variants of Playfair use "Q" instead of "X", but any letter, itself uncommon as a repeated pair, will do.
2.If the letters appear on the same row of your table, replace them with the letters to their immediate right respectively (wrapping around to the left side of the row if a letter in the original pair was on the right side of the row).
3.If the letters appear on the same column of your table, replace them with the letters immediately below respectively (wrapping around to the top side of the column if a letter in the original pair was on the bottom side of the column).
4.If the letters are not on the same row or column, replace them with the letters on the same row respectively but at the other pair of corners of the rectangle defined by the original pair. The order is important – the first letter of the encrypted pair is the one that lies on the same row as the first letter of the plaintext pair. To decrypt, use the INVERSE (opposite) of the last 3 rules, and the 1st as-is (dropping any extra "X"s, or "Q"s that do not make sense in the final message when finished).
## PROGRAM:
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define SIZE 30
void toLowerCase(char plain[], int ps) {
    for (int i = 0; i < ps; i++) {
        if (plain[i] >= 'A' && plain[i] <= 'Z')
            plain[i] += 32;
    }
}
int removeSpaces(char* plain, int ps) {
    int i, count = 0;
    for (i = 0; i < ps; i++)
        if (plain[i] != ' ')
            plain[count++] = plain[i];
    plain[count] = '\0';
    return count;
}
void generateKeyTable(char key[], int ks, char keyT[5][5]) {
    int i, j, k;
    int dicty[26] = {0};
    for (i = 0; i < ks; i++) {
        if (key[i] != 'j') {
            dicty[key[i] - 'a'] = 2;
        }
    }
    dicty['j' - 'a'] = 1;
    i = 0;
    j = 0;
    for (k = 0; k < ks; k++) {
        if (dicty[key[k] - 'a'] == 2) {
            dicty[key[k] - 'a'] -= 1;
            keyT[i][j] = key[k];
            j++;
            if (j == 5) {
                i++;
                j = 0;
            }
        }
    }
    for (k = 0; k < 26; k++) {
        if (dicty[k] == 0) {
            keyT[i][j] = (char)(k + 'a');
            j++;
            if (j == 5) {
                i++;
                j = 0;
            }
        }
    }
}
void search(char keyT[5][5], char a, char b, int arr[]) {
    int i, j;
    if (a == 'j')
        a = 'i';
    if (b == 'j')
        b = 'i';
    for (i = 0; i < 5; i++) {
        for (j = 0; j < 5; j++) {
            if (keyT[i][j] == a) {
                arr[0] = i;
                arr[1] = j;
            }
            else if (keyT[i][j] == b) {
                arr[2] = i;
                arr[3] = j;
            }
        }
    }
}
int mod5(int a) {
    return (a % 5);
}
int prepare(char str[], int ptrs) {
    if (ptrs % 2 != 0) {
        str[ptrs++] = 'z';
        str[ptrs] = '\0';
    }
    return ptrs;
}
void encrypt(char str[], char keyT[5][5], int ps) {
    int i, a[4];
    for (i = 0; i < ps; i += 2) {
        search(keyT, str[i], str[i + 1], a);
        if (a[0] == a[2]) { 
            str[i] = keyT[a[0]][mod5(a[1] + 1)];
            str[i + 1] = keyT[a[2]][mod5(a[3] + 1)];
        } else if (a[1] == a[3]) { 
            str[i] = keyT[mod5(a[0] + 1)][a[1]];
            str[i + 1] = keyT[mod5(a[2] + 1)][a[3]];
        } else { 
            str[i] = keyT[a[0]][a[3]];
            str[i + 1] = keyT[a[2]][a[1]];
        }
    }
}
void decrypt(char str[], char keyT[5][5], int ps) {
    int i, a[4];
    for (i = 0; i < ps; i += 2) {
        search(keyT, str[i], str[i + 1], a);
        if (a[0] == a[2]) { 
            str[i] = keyT[a[0]][mod5(a[1] - 1 + 5)];
            str[i + 1] = keyT[a[2]][mod5(a[3] - 1 + 5)];
        } else if (a[1] == a[3]) { 
            str[i] = keyT[mod5(a[0] - 1 + 5)][a[1]];
            str[i + 1] = keyT[mod5(a[2] - 1 + 5)][a[3]];
        } else { 
            str[i] = keyT[a[0]][a[3]];
            str[i + 1] = keyT[a[2]][a[1]];
        }
    }
}
void encryptByPlayfairCipher(char str[], char key[]) {
    int ps, ks;
    char keyT[5][5];
    ks = strlen(key);
    ks = removeSpaces(key, ks);
    toLowerCase(key, ks);
    ps = strlen(str);
    toLowerCase(str, ps);
    ps = removeSpaces(str, ps);
    ps = prepare(str, ps);
    generateKeyTable(key, ks, keyT);
    encrypt(str, keyT, ps);
}
void decryptByPlayfairCipher(char str[], char key[]) {
    int ps, ks;
    char keyT[5][5];
    ks = strlen(key);
    ks = removeSpaces(key, ks);
    toLowerCase(key, ks);
    ps = strlen(str);
    toLowerCase(str, ps);
    ps = removeSpaces(str, ps);
    generateKeyTable(key, ks, keyT);
    decrypt(str, keyT, ps);
}
int main() {
    char str[SIZE], key[SIZE];
    printf("Simulating Playfair Cipher\n");
    strcpy(key, "Monopoly");
    printf("Key text: %s\n", key);
    strcpy(str, "RAMKUMAR");
    printf("Plain text: %s\n", str);
    encryptByPlayfairCipher(str, key);
    printf("Cipher text: %s\n", str);
    decryptByPlayfairCipher(str, key);
    printf("Decrypted text: %s\n", str);
    return 0;
}

```
## OUTPUT:
![Screenshot 2025-03-19 142747](https://github.com/user-attachments/assets/75d62ffb-93c7-4352-956d-b47b3e4029e1)


## RESULT:
The program is executed successfully


## NAME: RAMKUMAR G
## REG NO: 212223220084



# Hill Cipher
Hill Cipher using with different key values

# AIM:
To develop a simple C program to implement Hill Cipher.

## DESIGN STEPS:
## Step 1:
Design of Hill Cipher algorithnm

## Step 2:
Implementation using C or pyhton code

## Step 3:
Testing algorithm with different key values. 

## PROGRAM:
```
#include <stdio.h>

int main() 
{
    unsigned int key[3][3] = {{6, 24, 1}, {13, 16, 10}, {20, 17, 15}};
    unsigned int inverseKey[3][3] = {{8, 5, 10}, {21, 8, 21}, {21, 12, 8}};

    char msg[4];
    unsigned int enc[3] = {0}, dec[3] = {0};

    printf("Enter plain text: ");
    scanf("%3s", msg);

    for (int i = 0; i < 3; i++)
        for (int j = 0; j < 3; j++)
            enc[i] += key[i][j] * (msg[j] - 'A') % 26;

    printf("Encrypted Cipher Text: %c%c%c\n", enc[0] % 26 + 'A', enc[1] % 26 + 'A', enc[2] % 26 + 'A');

    for (int i = 0; i < 3; i++)
        for (int j = 0; j < 3; j++)
            dec[i] += inverseKey[i][j] * enc[j] % 26;

    printf("Decrypted Cipher Text: %c%c%c\n", dec[0] % 26 + 'A', dec[1] % 26 + 'A', dec[2] % 26 + 'A');

    return 0;
}
```

# OUTPUT:
![Screenshot 2025-03-26 083533](https://github.com/user-attachments/assets/f2348885-0dfc-468f-aafb-c6b9138a921d)

## RESULT:
The program is executed successfully



## NAME: RAMKUMAR G
## REG NO: 212223220084



# Vigenere Cipher
Vigenere Cipher using with different key values

# AIM:
To develop a simple C program to implement Vigenere Cipher.

## DESIGN STEPS:
## Step 1:
Design of Vigenere Cipher algorithnm

## Step 2:
Implementation using C or pyhton code

## Step 3:
Testing algorithm with different key values. 
## PROGRAM:
```

#include <stdio.h>
#include <string.h>
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

    
}


```

## OUTPUT:

![Screenshot 2025-03-26 084300](https://github.com/user-attachments/assets/c5e41c20-3974-422f-a7d6-87555f6f00b2)


## RESULT:
The program is executed successfully


## NAME: RAMKUMAR G
## REG NO: 212223220084
# Rail Fence Cipher
Rail Fence Cipher using with different key values

# AIM:
To develop a simple C program to implement Rail Fence Cipher.

## DESIGN STEPS:
## Step 1:
Design of Rail Fence Cipher algorithnm

## Step 2:
Implementation using C or pyhton code

## Step 3:
Testing algorithm with different key values. 

## PROGRAM:
```
 #include <stdio.h>
 #include <string.h>
 int main() {
 int i, j, k, l;
 char a[20], c[20], d[20];
 printf("\n\t\tRAIL FENCE TECHNIQUE\n");
 printf("\nEnter the input string: ");
 fgets(a, sizeof(a), stdin);
a[strcspn(a, "\n")] = '\0';
 l = strlen(a);
 for (i = 0, j = 0; i < l; i++) {
 if (i % 2 == 0) {
 c[j++] = a[i];
 }
 }
 for (i = 0; i < l; i++) {
 if (i % 2 == 1) {
 c[j++] = a[i];
 }
 }
 c[j] = '\0'; 
 printf("\nCipher text after applying rail fence: %s\n", c);
 if (l % 2 == 0) {
 k =l / 2;
 } else {
 k =(l / 2) + 1;
 }
 for (i = 0, j = 0; i < k; i++) {
 d[j] = c[i];
 j += 2;
 }
 for (i = k, j = 1; i < l; i++) {
d[j] = c[i];
 j += 2;
 }
 d[l] = '\0';
 printf("\nText after decryption: %s\n", d);
 return 0; 
 }
```


## OUTPUT:
![Screenshot 2025-03-26 085141](https://github.com/user-attachments/assets/307f6fdd-9c18-4dd0-bf4f-6ae8567d5286)

## RESULT:
The program is executed successfully








