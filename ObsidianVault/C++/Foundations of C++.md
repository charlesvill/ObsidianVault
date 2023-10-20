#### parking lot: 
- what is the difference between constexpr and const?
	- a const initializiation can be deffered until runtime while a constexpr needs to be there compilation
##### Getting started: 
```cpp
#include<iostream>
#include "./std_header_files.h"

int main() {

	//some code here


return 0;
}
```
- the hashes there are known as preproccessor statements, it processes them before your file is processed. it basically pastes it in there. 
### Bjarne Stourstroup Ch 4
why use functional programming?
- separates computation logically
- makes it possible to use the functions in other places and 
- clearer/ease of testing
#### Types in C++
- for the most the same except that instead of a float for a decimal, you would use a double. 
- just like in C the different types take up specific amount of space: 
	- int - 4 bytes
	- char - 1 byte
	- bool - 1 byte
	- double - 8 bytes
	- string - ??? bytes
what are arrays called in c++?
- vectors
- they also have arrays but there are some differences: 
	- arrays are fixed in size need to be told their length from initialization
	- vectors can be dynamically changed and manipulated also memory allocation works automatically for vectors 
	- vectors know their size unlike arrays. has the method: `v.size() // return 4 if there are four indices`

initializing a vector: 
```cpp
vector<int> v = {5, 7,9, 4, 6, 8};
```
- in order to grow the vector you can use the method push_back() in dot notation on the vector variable 
sorting a vector: 
- you can use the method sort() to sort lexigraphically. however this is a mutable function member of vector. 
	- `vector<double> temps;  sort(temps);` make sure the vector goes in there. it does not attach with dot notaition to anything. 
#### functions in C++ 
- like C, you can declare a function after the main function however if you try to invoke it before it has been called you will need to place the function prototype or 'forward delcaration' before the main function.
##### switch statements
- for switch statements, if you wish to initialize a variable, you need to put it inside of a block. go figure. straight from the words of Bjarne himself. didnt give much of a reason besides the compiler said so. 
### Input/Output in C++
- for outputting to the terminal you cannot concat like you would in c with a + you have to use <<. for example: 
- `cout << "hello today's temperature is:" << double_temp << '\n'`
	- please note that each part you are trying to concatenate will need it's own << and also the terminating character needs the << and be surrounded by single ' '.
- for inputting to data, use cin but make sure the arrows are pointing towards where the data should be read into
- for ex: `cin >> int_name;` now this will read exactly one valid input into the variable. if you want to read multiple times, you'll need a vector and you will need a for or while loop to continue to read while there is valid input for example: 
```cpp
vector<double>temps
for(double input; cin >> input){
	temps.push_back(input);
}
```
- this will effectively continously read values into input and into the vector temps while values are being input
	- to terminate input, press ctrl+D in terminal on Unix and ctrl+Z on windows.
### ch 5 Errors
- being proactive about errors involves using the `error()` function with the message inside of it embedded where you would anticipate things to pass the compiler but nonetheless be a logical error given the context
	- *should be noted that this is a part of the books header file which is unclear if actually used by developers or only for the purposes of learning*
- direct vs indirect callers
	- errors that cannot be handled normally will throw an exception and can be called by any direct or indirect caller
		- direct: when function A calls function B and B has an error, A is the direct caller
		- indirect: if function C calls A whom calls B and the error is in B, then C is an indirect caller and the error will propogate up the call stack eventually to C
	- what do you call collections of data?
		- containers
	- what does the notation for range look like? `[0:5]` where the last number is not included 
#### detecting errors using try
- the try introduces our code to test and the catch will be a condition that would detect an error in the program
- some types in the standard library that aid in this: 
	- `out_of_range` from vectors
	- `runtime_error` will accept a string to aid with error handlers
ex: 
```cpp
void error(string s)
{
	throw runtime_error(s);
}
```

```cpp
int main()
{
	try{
		// our program
		return 0;
	}
	catch (runtime_error& e){
		cerr << "runtime error: " << e.what() << '\n';
		return 1; // 1 indicating failure
	}
}
```
		- the & is passing e by reference to the address of e (pointer shit)
			- notice the use of runtime_error type here
		- e.what() extracts the error message 
		- notice use of cerr instead of cout as cerr is used for error messages
- see chp 5 on erros 5.6.3 for more
- you can also use the type `narrow_cast<int>(2.9)` that will throw a runtime_error if an assignmnet or initiliaization would lead ot a changed value aka truncation
	- truncation is also known as a narrow conversion 
##### Template arguments 
- when you see the < ... > brackets as in vectors `vector<int>` they are examples of template arguments
	- the template argument specify to the type vector, what kind of data that type will pertain to

### ch 6 creating a program
think of developing a program as designing cars, you consider the wheels, seats engine, seats door handles and other pieces. just like manufactures dont build cars out of pure iron and wood, we should not bulid programs completely from scratch using just expressions, statements and types provided by the language
##### steps of development

- anaylsis
- design
- implementation
##### tokens and implementating tokens
- another way to describe it would be a *user-defined-type* 
- similar to a struct in C see [[C#struct]]
- like a struct you can put data in it and use dotnotation to access its member and assign them
```cpp
class Token{
public:
	char kind;
	double value;
};
```
we can copy over the objects over to over objects as long as the initializer is the same Token type
	- `Token tt = t;`
- we can also construct new tokens as such `Token t1 {'+'};` or `Token t2 {'8', 11.5}` where the first arg is the kind and the second is the value. 
- difference between this and structs is that you can also but functions as members.
	- in reality these are really just class objects, not so much structs (structs can only hold data, not functions as members)
- what is grammar and what does it have to do with parsing?
	- grammar is in the context of programming the process of creating rules for your program to abide by using a sort of technical notation such as the rules of the order of operation for a calculator
	- you formulate functions or instructions based on forcing the computer to follow this grammar. 
	- the process of appling your grammar implementation and putting data through it is known as *parsing*
- what does the `cin.putback(variable);` do?
	- if you read something from the input stream and you assign it to a variable and realize its a number or something and would like to assign it as a number, you can use the `.putback()` to literally put it back into the input stream and read it once more so you can assign it to a number type.
- more on classes: 
		- though not specifically introduced quite yet, classes aka objects have already budged their way in
		- how to define member functions outside of a class definition?
```cpp
class_name::member_name
```
-  the two sets of colons denotes the class from the member of the class. 
- why separate the member function definitions from the class definitions? i.e why define them outside of the class?
	- because it makes things easier to read and helps to put what the class members will do and then put the definitions or the implementation details of those things elsewhere
	- **look through 6.8 for reviewing pulling back and overview on your programs**
#### reflections on design patterns
- in regards to structuring this larger function where giving the computer a grammar or rules to follow, he doesnt define the single logical purpose of this function as one to parse all off the tokens in our calculator project. but instead he makes a function for each rule and includes it in the larger program.
- further Bjarne himself is seen making long switch statements stringing many case options for one result which previously I would have thought was messy and that many did not do that. stand corrected. 
- I'm also noticing that bjarne is mixing his declarations and expressions assignments and stuff so he's not grouping them by thing per say, atleast not at this time. will check back if he does. 
- Bjarne very much takes us through this iterative process of multiple steps that doesnt necessarily imply that programmers have to have all implementation details figured out on the first go. he attempts a version and sees an issue with it and then iterates on it again. even the mighty Bjarne doesnt fully anticipate every problem from the get go
- Bjarne mentions time and time again to avoid using complicated solutions and use library solutions whenever present because they have more time than you and have spent more time wokring on that than you. 
- *just thinking* rarely works, we cannot consier everything that will go wrong on the first run either, we need to try things and see what works best
- if a main loop is handling the general scaffolding of the program i.e getting things started, handling errors; if it also handles controlling the main calculator or program function loop perhaps its best to handle that in a separate function
	- try to emulate this in other programming languages even those that are dynamically typed and do not required things like int main () functions to get started. then separate the logical parts of your program stem by step in different functions. looking at the main function should look slightly like looking at a map
### Excercism notes
#### Namespaces
- the purpose of namespaces are to avoid collisions between  functions and programs that could share names. 
	- I guess things in C++ are not block scoped?
	- `namespace my_foo{ bool foo = false}`
	- `namespace other_foo{bool foo = true}`
	- you can nest name spaces and call specific functions by using the namespace *scope-resolution* operator `::` 
- see here: 
```cpp
namespace my_ns { 
	int foo() { return 44; }
	 namespace my_inner_ns { 
		 int baz() { 
			 return 90; } 
		} 
	
} namespace my_other_ns {
	int foo() { 
		return -2; 
	} 
} 

int myresult{my_ns::foo() + my_other_ns::foo() * my_ns::my_inner_ns::baz()};
```
- notice here the nesting of `my_inner-ns` and the accessor for the function inside of it, requires two sets of :: to access the correct scope. 
	- *remember to call the name of the namespace in the global space if you're trying to call one of the functions*
**this is actually pretty cool, because you can bring out deeply nested functions that you might need other places out the global scope and call them from there. not sure if other languages like javascrip allow you to do that without complex return systems**

#### Includes
- two ways to include libraries : `#include <cmath>` and `#include "myfile"` the difference is really in where it looks.
	- <> are for standard libraries and does not look in the local project files within the directory. 
	- "" are more for files you created or otherwise present in the directory that you want included. 
##### strings
- things like a string, need to be included in the standard library with `#include <string>` then the methods or *member functions* in those libraries can be accessed just like namespace accessors `::` i.e (`std::string message{"Hello World!"} ` ) 
	- notice here the curly braces used to initialize this string. this way of initialization is known as value initialization while using assignment operator '='  is known as copy initialization. this might need its own section to understand more about it. 
- note as well that when generating variables with types from the library you need to use the namespaces accessors as the data type: 
```c++
#include<string>

std::string string_example{"Hello World!"};

namespace logs(std::string message) {
	cout << message.substr(message.find(" ") + 1); 
}
```
- string methods: 
	- `string.substr(1)` use case is with taking two arguments 1. starting index and 2. how many characters to chop. if second arg ommitted, it will slice from the starting index to the end of the string and will return your new string. exactly same to javascript string method substr
	- `string.find("")` takes in a string and will return the index position of the beginning of named string

### Ch 8 Technicalities functions
- local functions nested into functions are not legal, dont do it
- make sure to declare non return type functoins with a void return type:
```cpp
void increase_power(int level) { ... }
```
#### passing values
- pass-by-value: give the function a copy of the value passed each time that the function is called a new copy is made
	- this will NOT change the original value
- pass-by-const-reference: instead of copying the value you can just pass the address of the original definition so you dont have to spend extra memory if thats not the purpose
	- the decision to not passby value comes down to whether you need to mutate the values 