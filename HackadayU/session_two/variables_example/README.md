Source:		https://hackaday.io/course/172292-introduction-to-reverse-engineering-with-ghidra

Author:		Hackaday.io

RE Tools:	Ghidra

<br>**Solution:**

Test the program:
    ./variables_example 
    --> Please prvide the 8 character keycode 
Open the program with Ghidra and inspect the main function with Function Graph tool and C decompiler

Inspect the decompiled P-code and rename the variables for better readability:

        int main(int argc,char **argv)
        {
          int 		ret;
          size_t 	len;
          int 		i;

          if (argc == 2) {
            len = strlen(argv[1]);
            if (len < 8) {
              puts("Too short, try again!\r");
            }
            for (i = 0; i < 8; i = i + 1) {
              if ((char)((char)(XorMe >> ((byte)(i << 3) & 0x3f)) + globalVar[i] + '\x01') != argv[1][i]) {
                puts("Improper character in keycode detected, try again!\r");
                return -1;
              }
            }
            puts("Proper keycode supplied, well done!\r");
            ret = 0;
          }
          else {
            printf("Please prvide the 8 character keycode");
            ret = -1;
          }
          return ret;
        }

The answer is encrypted in the line:<br>
   ` ((char)((char)(XorMe >> ((byte)(i << 3) & 0x3f)) + globalVar[i] + '\x01') != argv[1][i])`
<br>
    
to get the key, let's simplify the expression a bit:<br>
`    key_character = (XorMe >> ((byte)(i << 3) & 0x3f)) + globalVar[i] + '\x01')
`    <br>--> there should be 8 such key_character's..

What are then XorMe and globalVar?
    --> by left click on the global variables we can understand the types and values

globalVar is a string "KeYpress" - lets rename it into 'str' 

XorMe is a hex number 0xDEADBEEFFACECAFE. <br>To get the type, lets convert the number into decimal with the calculator: <br>
    https://www.rapidtables.com/convert/number/hex-to-decimal.html

    0xDEADBEEFFACECAFE = 16045690985305262846
        --> it's unsigned long


Lets decode the key with a simple C script:

    #include <stdio.h>


      int main(void)
      {
           int 			    i;
           unsigned long	            tmp;
           char			    new;
           unsigned long 	XorMe =     0xDEADBEEFFACECAFE;
           char str[]               =   "KeYpress";	

           for (i = 0; i < 8; i = i + 1)
           {
               tmp = XorMe >> ((i << 3) & 0x3f);
               new = (char)(tmp + (str[i] + 1));
               printf("%c\n", new);
           }
           return 0;
       }

Output will be:
    J
    0
    (
    k
    b
    $
    !
    R

In order to process the key in bash terminal, wrap it: 'J0(kb$!R'

./variables_example 'J0(kb$!R'
    --> Proper keycode supplied, well done!

