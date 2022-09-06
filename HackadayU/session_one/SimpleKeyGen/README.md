Source:		https://hackaday.io/course/172292-introduction-to-reverse-engineering-with-ghidra

Author:		Hackaday.io

RE Tools:	Ghidra

<br>**Solution:**

main function returns EXIT_SUCCESS if the checkSerial function returns 0.



For that following requirements should be fulfilled:

* There should be 1 argument
* key should be 16 chars long

the key is encrypted in this line of code:

    for (i = 0; len = strlen(key), (ulong)(long)i < len; i = i + 2) 
    {
        if ((int)key[i] - (int)key[(long)i + 1] != -1)
            return -1;
    }

* every next char of the key should be 1 step higher in ASCII than the previous.

--> the password is any ASCII sequence of 16 characters

Example:
    
    ./SimpleKeyGen abcdefghijklmnop
        --> Good Serial