ECE382_Lab2
===========
#Cryptography
##Objectives
Use pass by value and pass by reference subroutines to decrypt a message, given both the message and the key it was "XORed" with.
##Design
Because all the hardware was provided a flowchart of the assembly code is the only preliminary design needed to begin building the decrypt.
![alt tag](https://raw.githubusercontent.com/seanbapty/ECE382_Lab2/master/ECE%20382%20lab2%20-%20New%20Page.jpeg)
##Code
The actual decrypting of the message is done by 2 subroutines in the code. 
###Decrypt Message 
The first subroutine (decryptMessage) manages which byte to currently decrypt, where to store the result, and when to end the program by incrementing each of these values each time the a new byte is xor'd.
```
decryptMessage:
			call #decryptCharacter
	;mov.w 0(R5), 0(R6)
	inc.w R5
	inc.w R6
	inc.w R8
            ret
```
This subroutine is a call-by-reference subroutine because it is called when the program needs to adjust the memory reference for the message and message storage.  
###Decrypt Byte
The second subroutine (decryptByte) is responsible for XORing the key and the current encrypted byte. This routine also stores the decrypted value in RAM.
```
decryptCharacter:
	mov.b 0(R5), R9
	xor.b R4, R9
	mov.b R9, 0(R6)
            ret
```
This subroutine is call-by-value because it does not manipulate the memory location of message or the message pointers, but manipulates the values themselves.
