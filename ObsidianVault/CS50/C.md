- how to compile a file in cs50?
	- in the bash terminal, run make `filename` then run `./filename` 
- what is the print function?
	- `printf();`
	- *make sure to but make sure to put a `\n` to indicate a new line* 
- how do you initialize a script?
```c
int main(void){
//code here
} 
```
	this is your starter flag so to speak where all your code will be nested below it```
- how do you include the libraries in C?
	- you need to do `#include <stdio.h>` at the top of the file before the 
	- the difference between a library and a header is that the header is the mechanism to which a library is included into a file
- What are some important bash commands that we use in c?
	- cd, cp, ls, mkdir, mv, rm, rmdir
- what are some of the place holder variables when displaying return values?
	- %s - string
	- %i - integer
	- %c - char... etc
- In C, why do you need to use %\n everytime we want to print a couple integers?
	- printf takes multiple arguments and the first arugment says we are formatting the output into a string but taking in an integet to be converted
#### data type limiations in 
- you could hold 32 bits in an integer in C, roughly 4 billlion sized number
	- 2 billion in either the positive or negative direction
- the solution is to use a different data type, long integer
- in the placeholder for printf, what does `%.2f\n` mean as seen in this code: `printf("Sale Price: %.3f\n", sale`.
- The %f is normally for formatting printf for a float but the .x is for noting how many decimal places to use. 
- in C when listing parameters for a function, you must also indicate the data type that should be passed through as seen in. it's essentially like declaring a variable
#### loops in C
syntax: 
```c
for (int i = 0; i<3; i++){
printf("meow\n");
}
```
