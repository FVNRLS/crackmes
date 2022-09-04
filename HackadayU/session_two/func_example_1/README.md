Source:		https://hackaday.io/course/172292-introduction-to-reverse-engineering-with-ghidra

Author:		Hackaday.io

RE Tools:	Ghidra

<br>**Solution:**

Program takes the first argument and generates 2 strings with functions getUpperCase and getLowerCase:

    str_1 with uppercase letters and str_2 with lowercase letters

Here the requirements for a valid key:

1. Num. of uppercase and lowercase letters should be equal
2. Only alpha-letters are allowed

Examples:
  
    Aa
    AaAa
    BCmMcb
    
    ./func_example_1 BCmMcb
        --> Passcode generator passed, good job!
