#### parking lot: 
- what is the difference between constexpr and const?
	- a const initializiation can be deffered until runtime while a constexpr needs to be there compilation

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
##### Template arguments 
- when you see the < ... > brackets as in vectors `vector<int>` they are examples of template arguments
	- the template argument specify to the type vector, what kind of data that type will pertain to
- 