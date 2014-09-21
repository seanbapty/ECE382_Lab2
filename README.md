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
##Debugging
While debugging the code there were several problem points. First, in order to prevent registers from resetting to 0 when incremented, the must be incremented byte-wise. This was evident when the code was stepped through, because whenever the inc.b Rx came up, the register value would reset to 0 and then be incremented to 1. Additionally, I found it helpful to include a paper list of what registers were being used for what. This prevented confusion when deciding how to implement what was desired next. Finally, it is important to remember to be careful when using registers and subroutines, because initially a register was manipulated in both subroutines in addition to the "Main" thus destryoing the register.
##Testing
The testing for this program was simple. Since it was designed to decrypt a particular message, the message and key were loaded into ROM for the program to decrypt. It became apparent once this program was run correctly (after several mistrials) because 
the output in RAM was a comprehensible message reading a congratulatory note. It was determined that further testing would be unnessary, however, the program was also checked by hand XORing several bytes from the message with the key. 
