Source:		https://crackmes.one/crackme/6296c1ff33c5d45b75903c0f
Author:		b3nd3p
Level:		easy
RE Tools:	Ghidra

Solution:

1)	Test the program: 
	./first
	Type in any number and look at the output. Wrong output will give you the message: "try again!!!try more and u can"
2) 	Select all code and disassemble 
3)	Search for the string and it's location in the program --> function: bool check
4)	Navigate inside the function bool check(int param_1,int param_2)
	The function compares 2 parameters - user input and a secret key value. The key value is not published in the function, so we need to go 1 layer higher to understand where the parameters come from.
5)	In the program tree -> functions, open: main
	the function check is called in the main function after 2 parsing funtions: entry1 and input. input is the user input and entry1 should be the key value to compare with.
6)	Inspect entry1 function.
	Key value is hidden in this line of code:
	uVar2 = sum.0(1000,300,0x1e,7);	
	0x1e is hexadecimal and should be converted.
7) 	Calculate the sum: 1000 + 300 + 30 + 7 = 1337
8) 	Enter the key to ./first prompt
	--> Enjoy ))
	u can do this, congrut well done go next
