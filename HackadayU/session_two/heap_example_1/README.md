Source:		https://hackaday.io/course/172292-introduction-to-reverse-engineering-with-ghidra

Author:		Hackaday.io

RE Tools:	Ghidra

<br>**Solution:**

Program takes the first argument and extracts all uppercase letters in separate string str, calloc'ed on heap. 

Then counts the length of the result string.

<br>Here the requirements for a valid key:

1. In the argument should be exactly 12 uppercase letters
2. There should be only one argument

Examples:
        
    AAAAAAAAAAAA
    AAAAAAAAAAAAstring
    stringBAJSHDKASHDB....

    ./heap_example_1 stringBAJSHDKASHDB....
        --> The result is: BAJSHDKASHDB
