Source:		https://hackaday.io/course/172292-introduction-to-reverse-engineering-with-ghidra

Author:		Hackaday.io

RE Tools:	Ghidra

<br>**Solution:**

Key requirements:

* only 1 argument
* the key is 8 chars long
* the key is derived from this line:


        for (i = 0; i < 8; i = i + 1) 
        {
        if ((byte)("skeletor"[i] ^ mod[i]) != argv[1][i])
          puts("Wrong answer\r");
        }

to get the key lets write a C script:

    #include <stdio.h>
    #include <string.h>
    #include <malloc.h>
    
    int	main(void )
    {
        char 	*str = "skeletor";
        char	*key;
        int		len;
        int		i;
        char 	c;
        int     mod [8];

        mod[0] = 8;
        mod[1] = 9;
        mod[2] = 10;
        mod[3] = 11;
        mod[4] = 12;
        mod[5] = 13;
        mod[6] = 14;
        mod[7] = 15;

        len = strlen(str);
        key = malloc(sizeof(char)*len);
        i = 0;
        while (i < len)
        {
            c = str[i] ^ mod[i];
            key[i] = c;
            i++;
        }
        printf("%s\n", key);
        free(key);
        key = NULL;
        return (0);
    }

The answer is: {bogiya}

    ./skele {bogiya}
    Correct! You have the power!


    
    