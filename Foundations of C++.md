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
- you can use the method .sort() to sort lexigraphically
### Input/Output in C++
- for outputting to the terminal you cannot concat like you would in c with a + you have to use <<. for example: 
- `cout << "hello today's temperature is:" << double_temp << '\n'`
	- please note that each part you are trying to concatenate will need it's own << and also the terminating character needs the << and be surrounded by single ' '.
- 