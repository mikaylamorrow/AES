# Advanced Encryption Standard (AES) Java Implematation

I implemented AES in java. In the main method, I pass a 16-byte plaintext message and a 16-byte cipher key to the Encrypt method of the class AES.java. The method encrypts the message using the key and then decrypts it by calling the Decrypt method.

### Encryption Flow:
The encryption process starts in the method Encrypt. The input plain text is first converted into a 4x4 byte matrix. The following methods are implemented for the encryption process:
1. addRoundKey: this method XORs the input 16-byte input matrix with the 16-byte cipher key matrix.
2. shiftRows: this method performs circular shift of the 2nd, 3rd, and 4th rows of the input matrix. Each cell in each row is shifted by a specific number of shifts.
3. subBytes: this method substitutes each byte in the input matrix with a byte from the provided subBox matrix (look up table).
4. mixColumn: this method is the center of the AES algorithm. It provides the diffusion for AES by performing an invertible linear transformation on the matrix’s columns.
Given these methods, the encryption part of the AES algorithm can be divided into three parts:
1. In the first round, addRoundKey(keys[0]).
2. After the first round, 9 rounds of encryption are applied. Each includes shiftRows, subBytes, and mixColumns, and addRoundKey[1 - 9]. For each round, one of the key expansions is used.
3. In the final round, shiftRows, subBytes, and addRoundKey(keys[10]) are applied.
The outcome of the encryption phase is a cipher text.

### Decryption Flow:
The decryption is flow is just a reverse of the encryption flow. Using the methods invShiftRows, invsubBytes, and invMixColumns which inverse the effect of shiftRows, sybBytes, and mixColumns respectively. The process can be described as follows:
1. In the initial round, addRoundKey(keys[10]), invShiftRows, and invSubBytes are applied.
2. Then, 9 rounds of decryption are applied. Each round consists of addRoundKey(keys[9 – 1]), invMixColumns, invSubBytes, and invShiftRows.
3. A final round of addRoundKey(key[0]) is applied.

### Key schedule:
This method generates 10 different keys and store them in the keys arrayList. These keys are generated with the help of the rcon matrix. Each key is used in one round of the algorithm.

### Helper Methods:
I also created several helper methods to help me code this algorithm:
1. printMatrix: prints 4x4 matrices. Was used to debug the different steps of the algorithm.
2. byteMatrixToString: converts the 4x4 byte matrix into a string.
3. stringToByteMatrix: converts a string (input text and cipher key) into a 4x4 byte matrix.
4. swapMatrixElement: this method swaps any two elements of an input matrix. It was used in shiftRows and inShiftRows.
5. Galois: this method was used to do matrix multiplication neded in mixColumn and invMixColumn.

### Example input and output:
1- Input has a lower-case “s”

![image](https://user-images.githubusercontent.com/57641878/170394107-f97b418d-784e-4ba0-9366-54e87aa4ad31.png)

2- Changed Input to have upper-case “S”

![image](https://user-images.githubusercontent.com/57641878/170394124-f48111b4-6c1f-4f01-87ad-628b5a99876b.png)

