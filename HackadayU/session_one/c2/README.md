Source:		https://hackaday.io/course/172292-introduction-to-reverse-engineering-with-ghidra

Author:		Hackaday.io

RE Tools:	Ghidra

<br>**Solution:**

Valid Key Requirements:

* The password should contain at least 5 characters
* password should begin with 'h'
* password should have 'u' as 5th character

Examples:

    hacku
    hoiuu
    huuuu1233fdfdf12
    
    ./c2 huuuu1233fdfdf12
        --> Correct -- maybe we should pay attention to more characters...