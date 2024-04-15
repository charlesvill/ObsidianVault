#### parking lot: 
- what is the difference between constexpr and const?
	- a const initializiation can be deffered until runtime while a constexpr needs to be there compilation
- What are user defined operators and what are the use cases for them?
- what is operator overloading and what is the use case for them? and what is an example of how to do it?
	- referrenced in ch 9 of PPP2
- 
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
###### how to execute a file 
- using gnu compiler: 
	- `g++ hello.cpp -o hello`
	- `./hello`
### Bjarne Stourstroup Ch 4
why use functional programming?
- separates computation logically
- makes it possible to use the functions in other places and 
- clearer/ease of testing
#### Types in C++
- for the most the same except that instead of a float for a decimal, you would use a double. 
- just like in C the different types take up specific amount of space: 
	- int - 4 bytes
		 - by default will truncate a double or float 
	- char - 1 byte
	- bool - 1 byte
	- double - 8 bytes
		- you can use the cmath header function `ceil()` that will let you round up for an int
	- string - ??? bytes
 - type conversion: 
	 - for char to int: `char input = cin.get()// int digit = input - '0';`
	  - for int to char:  `char character = input + 'a';`
what are arrays called in c++?
- vectors
- they also have arrays but there are some differences: 
	- arrays are fixed in size need to be told their length from initialization
	- vectors can be dynamically changed and manipulated also memory allocation works automatically for vectors 
	- vectors know their size unlike arrays. has the method: `v.size() // return 4 if there are four indices`
 - arrays and pointers: 
	 - because of the fluidity between the data types of arrays and pointers, an array initiated with a pointer operator and data type can nevertheless still access its member through index notation. go figure. Dont know why: 
```cpp
int ARRAY_SIZE;
cin >> ARRAY_SIZE;
int *surveyData = new int[ARRAY_SIZE;
	for(int i = 0; i < ARRAY_SIZE; i++){
	cin >> surveyData[i];
	}
```
- notice ehere surverydata is a pointer but nevertheless can access its members with [i] as if it were a regular array of int type. 
	- also notice the use of the new keyword to dynamically create and thus allocate memory for an array
	- because its dynamically created you need to free the memory or else you''ll have leaks: 
		- `delete[] surveyData;` the delete[] operator used for arrays. 

initializing a vector: ;
```cpp
vector<int> v = {5, 7,9, 4, 6, 8};
```
- you can use vector_name.reserve(10) to generate a number of indexes ahead of time and while not necessary could help prevent your vector from having to resize itself as often.
- in order to grow the vector you can use the method push_back() in dot notation on the vector variable 
sorting a vector: 
- you can use the method sort() to sort lexigraphically. however this is a mutable function member of vector. 
	- `vector<double> temps;  sort(temps);` make sure the vector goes in there. it does not attach with dot notaition to anything. 
	insert to vector: 
		- use `pushback()` to add to the end or `insert()` for control at which index
- accessing members of vector: 
	- usual index syntax
##### loops in C++
- you have the options of:
	- do.. while()
	- for ()
	- for (variable : range)
	 - while()
- you can use `continue;` to skip one iterative cycle and `break` to break out of the loop entirely. 
- you can also skip the initializer if you dont need it( `for(;p!=0;++p){}`
##### functions in C++ 
- like C, you can declare a function after the main function however if you try to invoke it before it has been called you will need to place the function prototype or 'forward delcaration' before the main function.
##### switch statements
- for switch statements, if you wish to initialize a variable, you need to put it inside of a block. go figure. straight from the words of Bjarne himself. didnt give much of a reason besides the compiler said so. 
##### sorting in C++
- you have the option of `qsort()` and `sort()`
	- qsort: quick sort expects: 
		- (array, # items in array, sizeof(array data type), comparefunc)
		- the return value of the comparefunc should be an int
		- sorts based on returning a 0, -1 , or +1 to move pointer value
	- sort: (array, array + number of items, comparefunc)
		- sort actually has a built in compare function but allows you the use of a custom sorting function (example seen in qsort.cpp in repo)
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

### Pointers in C++
- Dffierence between a Pointer `int* num = 10;`
- and reference `int& num = num;`
- and finally dereference `int* ptr1 = &num; int value = *ptr1;`
- pointers will store the memory of the data
```cpp
int value = 10;
int* ptr = &value;  // <- pointer
int copy = *ptr;  // <- dereferencing
//copy == 10
int* tmp = nullptr;
```
- in order to initialize a pointer, you need to get the address using the & operator prefixed to the value whose address you want to store. &prefix means "address of" 
- The process of accessing the original value once again is called dereferencing. you set a variable of the same data type to the pointer that stores the address (with * prefix) "contents of".  
- you can also have a `nullptr` which points to nothing and is safe for initializing pointers like setting int to 0. 
- if you have a pointer pointing to a char or something in an array you can use ++p to move the pointer to the next element in the array: ``
##### specifying pointers through arguments
- when passing arguments might be unclear how to pass by reference and dereference at the same time. use suffix& instead to "refer to" the data wanting to pass: 
```cpp 
int[] x = {1, 2, 3, 4, 6, 7, 8}
for(int& x : v){
	++x;
}
```
- see without thereference you would be passing the value x by copying the value from v, but with the suffix& you are 'referring to' the value in v. memory performant
- note that you cannot reassign x's reference to something else after initialization

- You can have specific data type pointers `int*` or`char*` that store memory of data. You can also have void pointers
#### void pointers
- will store any data type without having to specify the type. however, you will not be able to dereference it wthout *type casting* which tells the compiler what to expect at th eaddress it tries to dereference at. 
```cpp
int num = 42;
void* voidPtr = &num;
int* intPtr = static_cast<int*>(voidPtr); <- casts to an int*
cout << *voidPtr; // 42 <- notice the dereferencing syntax here to get the value bc voidPtr still apointer so needs to be dereferenced. 
```
- to see type casting and void pointers in action, see the qsort example in samples folder in repo local files
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
- it might look like: `[{'h', 45.0}, {'z', 67.4}]` in an array of that stuct or token type
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
- representing special characters: use backslash escape character: `'\''`  for representing a single apostrophe
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
- Pass by reference: does not use const so you can actually change the value that you're referencing. 
	- how modifying values  by reference works:
```cpp
int i = 7;
int& r = i; //r references i
r = 9; //i is modified, becomes 9
i = 10; // i is now 10

cout << i << " " << r << '\n' //prints 10 10
```
	- as seen here both the reference and the i can change the value of i 
- *note: this does not work the same as it does with C*
	- the reference int& r is not valid c, that is strictly c++ sytax. would have to achieve this simliar thing using strict pointers. 
- Bjarnes rules of thumb when passing values: 
	- passby vlaue for very small objects
	- pass by const larg obj that dont need changing
	- return a result rather than modifying an object through reference argument
		- perhaps this means to make expressions happen on the return line without having to make a copy of the object if can be avoided. 
	- use pass-by-reference only when you have to.... 
	- when to use pass-by-reference? for functions that change several objects since only one return value and manipulating containers like vectors
##### constexpr functions
- at times we want calculations to be done at compilation instead of runtime and a function can do just that if its a constexpr function, here is the syntax: 
```cpp
constexpr double xscale = 10;
constexpr double yscale = 0.8;

constexpr Point scale(Point p) {return{xscale*p.x, yscale*p.y};};

```
- where p is a struct you can see constexpr being passed and they must be constexpr inorder to be calculated at compilation when called. 
	- things to note: it must not have side-effects aka modify values outside of it and obviously modify any of its arguments that are constexpr
##### static const initialization
- if we want evaluation at runtime, meaning using const instead of constexpr, but you still dont want to rerun a function multiple times to get a value, you can use a function that itself is a reference and use the `static` keyword seen here: 
```cpp
const Date& default_date()
{
	static const Date dd (...); //initialize dd first time we get here
	return dd;
}
```
	- note here the function is of return type Date struct and returns a reference to avoid copying and the static enables it to run once to generate and that's it
##### Namespaces
- functions organize blocks of code into logical action or goal 
- classes organize data and functions into a type and 
- namespaces organize chunks of functions and classes into parts of a program 
	- think namespace graphics_lib with classes and functions called Color, Shape, line, Text etc. 
	- just another way to organize logical parts of your code. 
- the real standard library way of using string is to name it out like this: `std::string h = "hello world"`
	- also std::cout<< "hello world" << std::endl;
- a shortended way of accessing member functions without being as verbose is by using a `using` declaration: 
	- `using std::string;`
	- now you can use string member type from std without having to write out the whole thing
	- introduced into your current scope
- even more global version of this is a `using` directive:
	- `using namespace std;`
	- this will bring all of the member functions from that namespace into the scope like cout, string, etc. 
	- not recommned to use unless its on widely known namespaces like std bc the source of those member functions can start to get cloudly if over used. 
### Ch 9 Classes, etc. 
#### User-defined types: Classes and std library types
- really the only built in types are char, int and double
- things like strings, vectors, ostream, Tokens, are all *user-defined-types* even though strings, vectors come from the standard library, they still need a user declaration to use them which makes them user defined. 
- What are the two kinds of user-defined types in c++?:
	- classes 
	- enumerations
##### classes: beginning
```cpp
class X{
public:
	int m;
	int mf(int v){return 2*v}
};	
X var; //variable var of type X
var.m = 7; //assign values to its member values
var.mf(9); //access and use the member functions
```

- implementation vs interface:
	- interface the public members that you can access for use throughout code base
	- implementation the private members that the other members might use and benefit from but have no access to on the outside of the class
		- *important to note that members are private by default unless otherwise defined as public:*
- what if you need something public by default?
	- a struct is public by default
- Class Members && constructors:
- Non constructor direction: 
	- for a class you will need a constructor to create an instance of that object in your code. however if you just want to access functions from a class you can also declare the functions static:
		- note*you will not be able to access non-static members*
		- the solution to this would be to 
```cpp
class MyClass {
public:
    static void myStaticFunction() {
        // Function implementation
    }
};

int main() {
    MyClass::myStaticFunction(); // Access the static function without creating an object
    return 0;
}

```
- Constructor route: 
	- most of the time your classes will need a constructor to have an instance of this class object. 
		- you can have a constructor that initializes variables or you have have a blank constructor like this: 
			- `Date(){};` if you dont need to initialize any variables and you just want to create an instance of the class and its member values and functions. 
				- if you dont use initializers you can declare a new instance of your class by running 
				- `Date date{};` 
```cpp
struct Date{
	int y, m, d;
	Date(int y, int m, int d);
	void add_day(int n);
}
```
- notice here the constructor is the member function with the same name so the struct type can be initialized as:
	- `Date today{2000, 05, 24};` 
	- notice in the declaration the use of parentheses to delimit the initialization
	- parenthesis are valid too but its c++ 98 (old)
	- *note: you can also use parentheses for built in types: int x {7};* but its weird
- defining members outside of the class:
```cpp
Date::Date(int yy, int mm, int dd)
	:y{yy}, m{mm}, d{dd}
{
...
}
```
- the weird syntax there is associating the values passed through the constructor with the actual member values in the class declaration. looks weird but I guess it works 
	- you could also manually set them in the brackets like `y==yy` but then you initialize with default values and then assign them the value. kinda like int x; x = 3; the former takes out a step
- Accessing member values on member functions defined outside: 
	- private values: 
		- 
- *rule of thumb on defining member functions inside or outside the declaration:* 
	- if the function is only a few lines long, but it inside. it could benefits from inline compilation which makes it faster especially if its used often
	- longer functions should be defined outside, longer functions dont benefit from inline compilation 
- Error handling: 
```cpp
void f(int x, int y)
	try{
		Date dxy{2004,04,03};
		cout << dxy << '\n';
		dxy.add_day(2);
	} catch(Date::Invalid) {
		error("invalid date");
	}
```
- note the try catch block before the scoping block and the catch with a call back function inside of it? need to come back to this. 
##### Enumerations
a simple user defined type that is a list of constants that can be used to store states or simple data types. 
a simple use case for this is to store the current state of something. like `mode = UPPERCASE`. this functionally has no difference between doing something like `mode = 1` for states however for obvious reaons the former is preferred for readability. 
- a simple implementation: 
```cpp
enum ModeType{UPPERCASE, LOWERCASE, PUNCTUATION}
int main(){
ModeType currentMode = UPPERCASE;
if(something){
	currentMode = LOWERCASE;
}
}
``` 
```cpp
enum class Month {
  jan = 1, feb, march, april ...
};
```
defined a type Month and when you initialize the first entry, the enum will automatically assign 2, 3, 4 etc for each consecutive value after that at compilation. 
	- you cant change the value of them but you can access some of its member values with a function: 
	` int(Month::jan)` to get the int value of it
- these class type enumerators are known as scoped enumerators, but they also have: 
- plain enumerators: 
	- do not use the 'class' keyword
	- you can access int values as it does an implicit conversion to int and does not require the use of class accessors as long as youre accessing in the same scope as where the plain enumerator was declared
		- ex: `Month m = feb;` `int n = feb` or `int n = m` it's converting the Month type to int
		- *want to be careful with plain enums bc of potential name collisions depending on where the scope is and so with the int type conversions. not as safe as enum classses*
##### class constructors & default values
- see 8.6.1 for default values in constructors 

### I/O Streams 
- what is a buffer? 
	- data structure that the ostream uses to store your data you give it while trying to comminucate with the operating system buffer is important for performance 
	- buffer is more visible in istream when youre inputting text, each key input is stored in the buffer until you hit enter 
#### opening a file: 
ifstream- an istream for reading from a file
ofstream - an ostream for writing to a file
fstream - iostream for both reading and writing to a file

```cpp
cout << "please enter input file name";
string iname;
cin >> iname;
ifstream ist {iname};
if(!ist)error("can't open input file ", iname);
```
	ifstream - the type
	ist is like cout or cin
##### stream states
- good() - operation succeeded
- eof() - end of input
- fail() - unexpected read like expecting an int and found an x
- bad() - disk read error and serious problem
- what would be the purpose in using the explicit fstream fs; fs.open("foo", ios_base::in) command?
	- when you dont have scope to implicitly close your file, you would have to pair it with the fs.close()
	- 
##### writing out to a file: 
```cpp
void outputDemo::fileWriter() {
  cout << "Enter output file name" << '\n';
  string filename;
  cin >> filename;
  ofstream ost{filename};
  if (!ost) error("cannot open file ,", filename);

  for (int i = 0; i < data.size(); i++) {
    ost << '(' << i << ')' << " " << data[i].xloc << '\n';
  }
  cout << "this should be done writing" << '\n';
}
```
- note here the ofstream ost{filename} this establishes the operand ost that a few lines below it writes out using ost << with the content
	- also note the error check (if no ost)throw error
### Ch 11 Programming Graphics
#### Getting started with graphics
- in order to get started with graphics, its important to understand the role of llibraries needed to be imported in order to have something displayed to the screen. 
	- libraries are needed due to the complexity and immensity needed to output graphics to the screen relative to the trivial in comparision programs you make in the terminal using neovim
##### libraries in C++ (or similar compiled language)
two kinds of libraries: 
	 - .dll= dynamic link library - these are precompiled and will run after your code is compiled. makes executeables smaller but will need to be present in order for your program to run successfully
	 - .lib = static link library - these essential include library code in with your compilation and ends with bigger executable files
- what is Cmake and what is its role in this?
	- Cmake is a tool that will adapt for your system and ide (if applicable) and will generate the make file for your system and code. the make file tells the compiler how your code should be stitched together and where the header files and libraries are that are essential to your project. 
		- knowledge of make files and cmake esseential in actual projects that utilize libraries.
- What is the Fast Light took kit?
	- a library for displaying graphics from code in the terminal. it will create windows and you can create graphics representations with it
- 