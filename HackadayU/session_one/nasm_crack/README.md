Source:		https://hackaday.io/course/172292-introduction-to-reverse-engineering-with-ghidra

Author:		Hackaday.io

RE Tools:	Ghidra

<br>**Solution:**

Navigate to the global variable passwd.
select the section and convert it to a char array.

Key = supersecret

    ./nasm_crack
    Enter your password: supersecret
        --> Correct!
