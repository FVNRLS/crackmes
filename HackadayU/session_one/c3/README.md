Source:		https://hackaday.io/course/172292-introduction-to-reverse-engineering-with-ghidra

Author:		Hackaday.io

RE Tools:	Ghidra

<br>**Solution:**

Valid Key Requirements:

* Only 1 argument
* Argument should contain at least 5 characters
* 3rd character should be 32 (in ASCII) bigger than 4th character

Examples:
    
    aaaAa
    bbcCa
    assSz23234dfdfdf

    ./c3 assSz23234dfdfdf
        --> Correct! You figured it out ... looks like we have to upgrade our security...