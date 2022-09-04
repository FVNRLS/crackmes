Source:		https://hackaday.io/course/172292-introduction-to-reverse-engineering-with-ghidra

Author:		Hackaday.io

RE Tools:	Ghidra

<br>**Solution:**

* Try the code:
  * ./loop_example_1
    * Please provide a string!
  * ./loop_example_1 12
    * Wrong length! Try again!
  * ....
* Open the program with Ghidra and inspect the main function with Function Graph tool and C decompiler 
* Inspect the decompiled P-code and rename the variables for better readability:



    int main(int argc,char **argv)
    {
        int ret;
        size_t len;
        int i;
        int cnt;
    
        if (argc == 2) 
        {
            len = strlen(argv[1]);
            if ((int)len == 15) 
            {
                cnt = 0;
                for (i = 0; i < 15; i = i + 1) 
                {
                    if (('@' < argv[1][i]) && (argv[1][i] < '['))
                        cnt = cnt + 1;
                }
                if (cnt == 8) 
                    puts("Congratulations, access granted!\r");
                else
                    puts("Not quite what we\'re looking for ... maybe try again?\r");
                ret = 0;
            }
            else 
            {
                puts("Wrong length! Try again!\r");
                ret = -1;
            }
        }
        else 
        {
            puts("Please provide a string!\r");
            ret = -1;
        }
        return ret;
    }

* Let's extract the requirements from the C code --> the key should contain:
  * exactly 15 characters
  * 8 characters should be in ASCII between @ and [
    * --> 8 alphanumeric characters in uppercase
  * another 7 characters can be anything else
  * the position of the characters doesn't matter

* --> different keys combinations are valid:


Examples:

    AAAAAAAAaaaaaaa

    BBBBBBBBbbbbbbb
    
    cccccccZZZZZZZZ

and so on...

    ./loop_example_1 AAAAAAAAaaaaaaa
    Congratulations, access granted!
