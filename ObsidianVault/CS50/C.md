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
	- working with ints, if you want to display a float, you could apply a conversion of those ints by applying an operator thats a floating point (i.e /3.0). 
		- you could also perform what's called typeing which is when you apply an operator with the data type (float)  in parentheses
- In C single vs double quotes are not treated the same `''` vs `""` 
	- single quotes meant to represent a char and double quotes meant to represent a string
	- obviously strings can be used to represent chars but not vice versa
#### loops in C
syntax: 
```c
for (int i = 0; i<3; i++){
printf("meow\n");
}
```
- for loops will run the code before iterating up from 0. 
- decrementing backwards creates some strange behavior when the value of the integer becomes negative with the integer data type
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
#### Arrays
```
```
- declaring an array, ` int scores[3];` in C this tells the computer to hold the bits of memory for 3 numbers in an array that you can add in later
- strings are really just arrays of char, but they always have an additional byte of memory at the end that stamps that its the end of the string a `\0`
- for printing out an array of chars aka a string, i could do printf `"%c %c %c",s[0],s[1],s[2] `;
	- you could print out the 4th as `s[3]` to print out the 0 that is set at the end of strings
- how would you count the chars in a string?
	- you would iterate over the index numbers using a while loop and it's while the `[n] != \0` and i++; until the index number results in that terminating character that denotes the end of a string
- What is a library for strings?
	- string.h - has a method to tell you the sting name
- how to check the length of a string using the string library?
	- the "string.h" library includes a function to check the array length
	- `int length = strlen(name);` this will return an integer that can be used as any other integer.
- ctype.h
- how could you check if a char is upper case?
	- if(`char[n] >='a' && char[n] <='z'`) this will allegedly tell if it's uppercase
- creating static arrays - something that is not meant to be changed
	- you can use curly brackets and not have to put the size of the array 
		- `int numbers[] = {20, 10, 330, 35};` noting here the lack of initializing the size of the array and listing the exact numbers that will be in the array.  
#### command line arguments
 - when you want to pass through arguments into your program similar to the way you would a command in bash terminal, you can change the int main (void)  status to :
	 - `(int argc, string argv[])` this will allow you to pass through for example when your name if inside your main you printf out the `argv[1]`. 
	 - `argv[0]` contains the name of the file, so if you want to access the arguments you passed you'll need to start the index at 1.
	 - it seems like the first parameter argc counts the number of arguments you're passing through to tell how big the array should be
#### Exit statuses
- when your program ends successfully, it returns a secret number to indicate that it ran successfully and any other number means likely that something went wrong
- the int in `int main (void)` main will always return an integer, 0 by default. again hidden
	- the command `echo$?` will return the exit status of your program, usually one, but you can change it by changing the return to 1 or something else.
## Algorithms 
- some specific kind of algorithm is a searching algorith 
- binary search: 
	- a search algorithm that has a starting point and then goes one of two directions, left or right in the array based on stipulated rules example of 0(log n)
	- binary search however needs to be sorted, and for that you'll need a sorting array...
- Running time
	- the way that computer scientests describe the time it takes to solve a problem using an algogrithm
- big O notation
	- O(n^2)
	- O(n log n)
	- O(n) - linear number of steps where n is the input problem
	- O(log n)
	- O(1) - finite number of steps
- Upper and lower boundary for best/worst case scenario 
	- omega symbol  The best case scenario$$lower bounds      \Omega$$
		- in the best case it was omega(1) because she could have gotten lucky and opened the correct door on the right one
	- Theta Symbol when the upper bounds and the lower bounds are actually the same
		- for example counting every object would always take the same number of steps, it's the same you cannot get lucky or skip anyone
#### Searching
- comparing arrays of strings does not work with a simple "=" because each string is in itself an array. you need the `<string.h>` library called `strcmp()`. 
	- takes two arguments one for each of the strings being compared
	- returns a 0 if same 1 if one of them is alphabetically before the other and -1 vice versa.
	- similar to the javascript function `localeCompare(inputstring)` see [[Intermediate Javascript]]
- if you over iterate in an array, you will be accessing memory that you should not be accessing, you'll get an error, becareful not to do that.
- once you have found what you're looking for in an array, besure to break out of it by breaking out or returning 0 if all went well.
	- otherwise it will keep running
- You can call an array a basic data sctucture where you can keep much of the same kinds of data
#### struct
basically a object like in javascript, a data scrutcure that stores different things
	syntax:
```c
typedef struct
{
	string name;
	string number;
}
person;
```

- the typedef and struct are declaring the data dype and the person at the end is the name of the struct the strings are the things being put into the struct
- this goes above the main function
```c
person people[2];
people[0].name= "David";
people[0].number= "+1-909-908-9084";
```
- to add data to it, you can declare a separate array of type name of the struct and then access the data inside of it using dot notation
#### sorting
- when choosing a sorting algorithm to implement, there are compromises that you have to consider for any one. for example, bubble will sometimes be slower than selection even though theyre about the same big o notation however, if the list is sorted or partially sorted, bubble will be much faster. 
- and when considering very long lists, and they are unsorted, something like a merge sort will be muct faster, but at the cost of greater memory and space because of the auxiliary arrays needed to be made in storage to merge partitions of the list
- selection sort - will sift through the entire list and find the smallest value, then will swap values with the current iterator value
	- O(n^2) very slow upper bound, omega bound is still the same bc for each index value it needs to iterate over to make sure they are in the same spot.
	- so it is theta (n^2)
- bubble sort - focus on solving a smaller problem at a time, the bigger value will sort of bubble to the top
	- make sure to do n-2 for the iterator because you're comparing two things and if you're comparing the last one and you try to look beyond the length of the array you will get an error
	- the upperbounds are on O(^2) 
		- the lowerbounds are on O(n) because if they are mostly sorted, it has a break point where if it runs through and it does not sort anything any more then it will stop, unlike the selection sort
- Merge sort - divides the array into two and sorts the left and right side and then merges the list by comparing the first index of each of the sorted halves and then adds them to a new array sorted. 
	- achieves run time of O(n log n) quicker than a bubble or selection sort 
		- both the omega and the theta run time is O(n log n) because it has to run through the entire recursive process given the n length of numbers to be sorted regardless if they're previoulsy sorted or not, thus, hypothetically, you could have bubble sort finish quicker than merge sort
#### Recursion
- when you have a stop feature for the recursion you call it a base case
- with recursion, you could increase the call stack without necessarily executing the desired code until you reach the base case. then once you return from that last function call, you still the other function calls in the stack and will execute the others 
- Acheiving the *merge sort* 
	- recursively call for the function to sort the left and right half and then merge 
	- ex 7254
		- 72|54
			- 7|2|54
				- 27|5|4
					- 27|45
						- 2457
	- this example shows the process of splitting the sides until you have only one (the base case) 
##### Lab/Problem set week 3: algorithms
- you can time the speed of the programs using time ./programname . it might be a command line command provided by cs50
- two dimensional arrays: 
	- basically an array of arrays that allows for matrices to be implemented into code
	- syntax is: `int two_dim_array[R][C]`  where the r is the number of rows and the c is the number of columns. thankfully, it's written in the same order as the grid paradigm in javascript where the declaration of the grid template comes in rows first and then the columns. atleast there is some continuity there
	- adjacency matrix - a way to represent a graph where a 1 indicates two points are connected and a 0 indicates that they are not
	- in order to determine which one does not have an arrow pointing to them is to see which of the elements does not have a 1 or a truth value 
		`001`
		`010`
		`011`
		here the rows are represented by i and the columns by j with the syntax `2darr[i][j]` 
		the column j has the 0s without any 1s.
## Memory
- what is a bitmap?
	- type of image that use binary to represent grid of pixels in a coordinate type of arrangment
- hexadecminal: 
	- our decimal uses 10 digits and then we have to reuse them to represent higher numbers (124)
	- hexadecimal uses actually 16 digits before it needs to reuse any. it uses letters once it runs out of decimals
	- the biggest digit in hexadecimal is ff which is 255 which is why you have 255 possible 
	- How to count to 10 using hexadecimal: 01 <- 1 , 02 , ... 0A <- 10 after 09 uses letters and 16, 10 <- the placevalue in front represents the competion of the first base 16. 
	- What is 0x that is seen in memory addresses? its a humna convention to let yoj know that it's hexadecimal toi not make it confusing. 
	- when working with rgb values in bitmaps, you could either enter an integer or the hexadecimal equivalent 
- Memory Addresses
	- `&` - provides the address orf something stored in memory
	- `*` - instructs the compiler to go somewhere in memory
#### pointers
- very easy to break programs with pointers. 
	- its really just a variable that contains the address of some value. an address to something in memory
	- just literally points to something else. 
- up to this point, we have been passing data by value
	- what this means is copies of data
	- 
- `int n = 50;` -> `int *p = &n;` 
	- the star clues the compiler that we're storing an address of something
- Strings in memory - the array members have their place in memory but the variable s is also something, but it is stored in memory as actually pointer that points to the address of the first index number
	- it after all has the null terminating character that tells it when the array is over.
	- essentyially then the variable for the array s is really a pointer
- Strings are not really strings per say as a word in memory. it's really an array of chars its a 
- using string as a keyword in C was a training wheel. an abstraction for us, it used a struct like so: `typedef char *string;` 
- how to print the address of a pointer? 
	- you need to use `printf("%p", x)`  thats the new placeholder for pointers
- new way to print out strings: `char *s = "hi"; \n printf("%s", s);`
	- here the %s still prints out the whole string but if I change the placeholder to %p it will instead print out the address of the first char
	- printf is smart because if you put a `*s` as the variable to print out, it will actually print out the letter at the address, but printf knows that it wants the string and just wants the address and knows to print out the subsequent chars until it hit s the null character.
- Whiat is the power and the danger of C? 
	- well with pointers you can poke around memory past what is allocated for your program. so hypothetically a sophisticated hacker can inject something into your C program and poke around the other areas of memory looking for credit card information or other kernel information, bad things in general. 
- in something like strcmp() the compiler knows to look at the different memory addresses to two variables that hav ethe same contents and compare the contents. the reason why just == doesnt work to compare strings on its own is because its comparing the address of the first char which is not the same because they're different variables
#### malloc and free
- `malloc` memory allocation 
- `free` is when youre done with it and it frees the memory allocation for something
	- new library `<stdlib.h>` that lets me manage my memory
	- copying a string over involves allocating memory for the length of the string plus 1 (for the null character) and then assign each index to the index of the previous string
	- strcpy(destination, source) is a replacement for that process luckily abstracted for us. 
- *optimization tip: if you have a function like strlen() in a loop you are uselessly using more memory than necessary so you can define two variables in a loop separated by a comma next to the i iterator so it does not call the function over and over again.* 
- what is the difference between `nul` and `null`? 
- other good practices: 
	- if you use get string but use too much memory, you could cause a crash so you should put a conditional if get string == null return 1; 
	- then at the end of the program just to be clear return 0; 
- Malloc memory Laws
	- at the bottom of your program you should always free your memory when using malloc
	- something to note is that when your program terminates it will automatically free the memory but if it is somethign that is running all the time then you need to be freeing the memory
	- do not need for get_string because it's already programmed to rid the memory on its own
##### valgrind 
checks for memory leakage you can look at the end and see how many bytes went unfreed or leaked
##### garbage values
if you initialize an array with 1000 indexes but dont assign values you might get random numbers there that were left over from previous functions or other things in your computers memory, those are called garbage values. you should not initialize values without assigning them something because it could fuck with your shit

##### swap 
- when it comes to computer memory, there are different sections or areas of memory that are accessed for different things. for example, at the top highest priority if you will, is machine code that is quickly accessible by the cpu. then you have global, and then you have the heap. heap is essentially like a heap of memory, a chunk of memory and thats where when you call malloc, it carves out memory. it carves from top to bottom. below the heap is the stack memory. 
	- the stack memory is for functions and temporary variables that are called within functions. and this memory works from bottom up. 
- both heap and stack memory build up in each others colliding direction and problems will arise if too much is allocated in either one to make them collide. its our job to minimize the possibility of that happening. 
