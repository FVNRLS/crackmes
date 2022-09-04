Source:		https://hackaday.io/course/172292-introduction-to-reverse-engineering-with-ghidra

Author:		Hackaday.io

RE Tools:	Ghidra

<br>**Solution:**

Program takes 2 arguments:

index and keyword.

Index is given in the first condition 

-> there are 5 keywords possible

Keyword are derived from the keywords global variables

--> should be casted to char **

So keywords are:
hackadayu"
"software"
"reverse"
"engineering"
"ghidra"

After the calculation with the keywords we get the real keywords.

For that, we can simplify the decompiled C function and write following C script.

    #include <stdio.h>
    #include <string.h>

    int	main(void )
    {
    char *keywords[5] = {"hackadayu", "software", "reverse", "engineering", "ghidra"};
    int		i;
    int		j;
    int 	len;
    char 	curr_char;
    char 	next_char;

	i = 0;
	while (i < 5)
	{
		len = strlen(keywords[i]);
		j = 0;
		while (j < len)
		{
			curr_char = keywords[i][j];
			if (j == len - 1)
				next_char = keywords[i][0];
			else
				next_char = keywords[i][j + 1];
			if (next_char < curr_char)
				curr_char -= next_char;
			else
				curr_char = next_char - curr_char;
			curr_char += 96;
			printf("%c", curr_char);
			j++;
		}
		printf("\n");
		i++;
	}
	return (0);
}

Output:

    gbhjccxdm
    dincvqmn
    mqqmanm
    igbei`miegb
    aaenqf

So the valid combinations are:
        
    0 gbhjccxdm
    1 dincvqmn
    2 mqqmanm
    3 igbei`miegb
    4 aaenqf

    ./array-example 3 'igbei`miegb'
        --> Congratulations, you've unlocked the code for value 4, can you get them all?
    
