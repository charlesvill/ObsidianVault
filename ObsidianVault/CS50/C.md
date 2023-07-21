### Lesson 1
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
- trunctations- when you dont have memory space to display a longer number and so part of it gets chopped off. 
	- like the calendar in 1999 that code was limited to truncate in the year 2000 they thought they would break
	- they think this is going to happen again for computers counting the number of seconds since 1970s because passing 2 billions seconds aka the limit of 32 bit computers. 
	- 
#### loops in C
syntax: 
```c
for (int i = 0; i<3; i++){
printf("meow\n");
}
```
### Lesson 2 Arrays 
#### On Compiling
- what is clang?
	- a popular compiler that stands for c language
	- cs 50 uses clang under the hood but automates alot of the process with our "make" command
	- in reality, any third party library like `cs50.h` would need to be linked in the compiler so it finds the binary information for the contents of that third party library. 
	- for example: this is what that command line looks like to compile a simple hello world file:
```bash
clang -o hello hello.c -lcs50
```
- this certainly has more arguments than make 
- What does the process of compiling look like? there are for steps:
	1. Preprocessing - things that need to be analyzed before anything else. ex. the header files that need to processed before hand. 
		1. looks for a folder usually called usr/include that has these header files
		2. itll go into the file and copy and paste the contents of that file, we do not see it, but that is what is happening behind closed doors.
			1. there will alot of code in your file only if you're doing hello world because of all of the things that are imported through the standard library even if you dont use it
	2. Compiling - when it converts the c language to assembly language. closer to machine instructions to call functions move/subtract memory
	3. Assembling - When it converts into machine code, binary
	4. Linking - combine the binary of the code you actually wrote, the code of the library imported, and the standard library and links it all together. 
- This whole process shortened down to just compiling. 
	- we are using web to connect to cs50 coding environment, but those 0s and 1s exist somewhere on a server computer that is handling it for us and streaming it for us over the internet. 