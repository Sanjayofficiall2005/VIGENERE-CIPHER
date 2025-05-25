# EX.NO:4- VIGENERE-CIPHER
## Submitted By: SANJAY M
## Reference Number: 212223230187
## AIM:

To implement the Vigenere Cipher substitution technique using C program.

## DESCRIPTION:

To encrypt, a table of alphabets can be used, termed a tabula recta, Vigenère square,or Vigenère table. It consists of the alphabet written out 26 times in differnt rows, each
 
alphabet shifted cyclically to the left compared to the previous alphabet, corresponding to the 26 possible Caesar ciphers. At different points in the encryption process, the cipher uses adifferent alphabet from one of the rows. The alphabet used at each point repeating keyword.depends on a Each row starts with a key letter. The remainder of the row holds the letters A to Z. Although there are 26 key rows shown, you will only use as many keys as there are unique letters in the key string, here just 5 keys, {L, E, M, O, N}. For successive letters of the message, we are going to take successive letters of the key string, and encipher each message letter using its corresponding key row. Choose the next letter of the key, go along that row to find the column heading that	atches the message character; the letter at the intersection of
[key-row, msg-col] is the enciphered letter.


## ALGORITHM:

1. Input: Plaintext (P) and key (K).
2. Repeat: Repeat the key K until it matches the length of P.
3. Shift: For each character in P, shift it by the corresponding key character
(using modulo 26).
4. Encrypt: For each letter in plaintext P[i], compute C[i] = (P[i] + K[i])
% 26, where P[i] and K[i] are converted to numbers (A=0, B=1, ..., Z=25).
5. Output: Combine the resulting characters to form the ciphertext (C).
6. Finish: Return the ciphertext.


## PROGRAM
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>
void sanitizeKey(char key[]) {
int j = 0;
for (int i = 0; key[i] != '\0'; i++) {
if (isalpha(key[i])) {
key[j++] = key[i];
}
}
key[j] = '\0';
}
void vigenereEncrypt(char text[], const char key[]) {
int textLen = strlen(text);
int keyLen = strlen(key);
int keyIndex = 0;
for (int i = 0; i < textLen; i++) {
char c = text[i];
if (isalpha(c)) {
char keyChar = toupper(key[keyIndex % keyLen]);
if (isupper(c)) {
text[i] = ((c - 'A' + (keyChar - 'A')) % 26) + 'A';
} else {
text[i] = ((c - 'a' + (keyChar - 'A')) % 26) + 'a';
}
keyIndex++;
}
}
}
void vigenereDecrypt(char text[], const char key[]) {
int textLen = strlen(text);
int keyLen = strlen(key);
int keyIndex = 0;
for (int i = 0; i < textLen; i++) {
char c = text[i];
if (isalpha(c)) {
char keyChar = toupper(key[keyIndex % keyLen]);
if (isupper(c)) {
text[i] = ((c - 'A' - (keyChar - 'A') + 26) % 26) + 'A';
} else {
text[i] = ((c - 'a' - (keyChar - 'A') + 26) % 26) + 'a';
}
keyIndex++;
}
}
}
int main() {
char key[100], message[1000];
printf("Enter encryption key (only letters): ");
fgets(key, sizeof(key), stdin);
key[strcspn(key, "\n")] = 0;
sanitizeKey(key);
if (strlen(key) == 0) {
printf("Error: Key cannot be empty after removing spaces!\n");
return 1;
}
printf("Enter message to encrypt: ");
fgets(message, sizeof(message), stdin);
message[strcspn(message, "\n")] = 0;
printf("\nOriginal Message: %s\n", message);
vigenereEncrypt(message, key);
printf("Encrypted Message: %s\n", message);
vigenereDecrypt(message, key);
printf("Decrypted Message: %s\n", message);
return 0;
}
```
## OUTPUT
![image](https://github.com/user-attachments/assets/36d3c396-1360-4bf9-9e31-7ad7a83798b6)


## RESULT
The program is executed successfully
