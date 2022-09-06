Source:		https://hackaday.io/course/172292-introduction-to-reverse-engineering-with-ghidra

Author:		Hackaday.io

RE Tools:	Ghidra

<br>**Solution:**

Valid Key Requirements:

* Only 1 argument
* Argument should contain at least 9 characters
* every key character is switched 2 positions higher in ASCII (similar to caesar cipher)

to decode the key, let's write a simple C script:

#include <stdio.h>
#include <string.h>
#include <malloc.h>

    int	main(void )
    {
        char 	*str = "hackaday-u";
        char	*key;
        int		len;
        int		i;
        char 	c;

        len = strlen(str);
        key = malloc(sizeof(char)*len);
        i = 0;
        while (i < len)
        {
            c = str[i] + 2;
            key[i] = c;
            i++;
        }
        printf("%s\n", key);
        free(key);
        key = NULL;
        return (0);
    }

--> key = jcemcfc{/w

    ./c4 jcemcfc{/w
        --> Correct! You've entered the right password ... you're getting better at this!
