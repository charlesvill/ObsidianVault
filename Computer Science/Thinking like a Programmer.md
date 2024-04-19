- notes on the book by Anton Spraul

- why people struggle with problem solving
	- people percieve that they didnt think about a possible operation or tool that could have been used or applied in the situation
	- by writing out all possible actions and tools we can find solutions 
	- restating the problem in more formal terms can aid with this
		- what does it mean to restate the problem in more formal ways?
			- list out possible operations in more generic terms:
				- with the fox goose, corn ex, instead of (take goose across river) think(row across each shore) and (if boat empty, load something to take across), and (if boat full, unload something)
				- essentially, keep the focus on thinking about the problem, not the solution. like discussing the problem with another peer, rubber ducking as coined in CS50
	- lessons from tile puzzle: a larger problem made easier by breaking it up into smaller problems
	- lessons from the sudoku puzzle: always look for the most constrained part of the problem and flesh that out first
	- lesson from the quarsi: look for analogous problems and bridge knowledge between the solution to the analogous situation to the current problem
#### General techniques
##### always have a plan
- plans might often be thrown out or need to be altered or changed however it is always important. 
- part of it includes having measurable goals along the way, dont make completing the entire problem the goal. 
##### restate the problem
- many programmers skip this because it doesnt have to do with programming a solution
	- this was because it wasnt part of the plan, so thus, restating the problem should be the first step of your plan
- helps to think about the problem in your and reason about what its asking and illuminates things about it you might not have if you just jumped in
##### divide the problem 
- after understanding the problem boil down the problem into either steps or facets of the problem that might have to come together at some point
- this also includes listing out what skills would be needed to solve the problem
- chunk it into smaller pieces that require a more trivial solution
##### start with what you know
- if you already know how to set up the skeleton or some parts of it, start with that
- this also includes applying what you know and how you could use it before researching a technique or looking for a solution online
	- thinking using with whats in your head also goes with having a plan
##### reduce the problem
- add or remove constraints to create a micro controlled enviroment to learn more about a part of the problem that could provide insight or even the solution to the problem
##### look for analogies
- think of how the problem could be related to another problem that you have solved, or even how its different.. what components make this problem different and what make them similar.. illuminates a focal point perhaps
- avoid relying on code found outside if you could not write that code yourself.. will not count towards a solution you can add to your bank of potential future analogies 
##### experiment
- does not involve guessing, it involves taking a small piece perhaps of the problem and hypothesizing a pattern of behavior and creating a micro environemnt where you can test that to learn more about it,
- includes the use of debuggers
##### dont get frustrated
- instead of stubborningly persisting on a problem when already frustrated with, take a break by either going for a walk or working on another problem that isnt related to that one while you cool off

### Ch 2 pure puzzles

#### the importance of code reuse: 
- this builds on [[#look for analogies]] but always store your code solutions in a way that would be accessible in the future because it will save from having to relearn something. 

### Ch 3 problems with arrays
- what does it mean to refactor something so that it scales better with larger datasets? 
	- for example you might have a working algorithm to find the mode of a dataset but its time complexity might be something like O(n^2) and on a bigger data set could slow things down considerably. then you would instead refactor to get an algorithm that has a better time complexity like linera O(n) example can be seen in mode findig example

### Ch 4 solving problems with pointers
##### review on pointers
you can reassigna pointer to another pointer: `int * intPointer; , variable1 = &var2; , intPointer = variable1;`
###### allocating memory
- you have to use the *new* keyword: `double * point = new double;` where new datatype;
- to deallocate: `delete doublePointer;` 
###### dereferencing
```cpp
*doublePointer = 35.4;
double localDouble = *doublePointer;
// you can directly modify the contents of it with the pointer operator in the front of the variable wihtout having to reassign it to something else first. 
```

what are some of the benefits of Pointers?
- they allow you to determine the size of a data structure during runtime so that the footprint perhaps of your data structue can be more efficient and use only what you need
- they allow a data structure to be resizable 
- memory sharing- instead of passing by copying a value, you can pass by reference and share the memory blocks and thus improve the memory footprint of your application even more. 
**note**: there is no difference between `int & x` , `int& x` , or `int &x` . they are all the same thing and mean the variable of data type int, will pass through the reference to its place in memory as opposed to making a copy of it. 
###### Memory sharing
- when you pass by memory, you make a copy of the 64 bit pointer instead of the larger data type. however this means that the memory is shared between those two things and can mutate the original block of memory. When you want to pass by reference but want to specify that the memory should not be rewritten, preface the variable name with the keyword 'const'
##### When to use Pointers
- pointers can come with potential drawbacks and only should be used when appropriate. 
- in general pointers should be used when we require one of more of the benefits of pointers. 
	- you have a data that needs flexibility of being resized during runtime
	- large objects that need to be passed around to different objects and functions
	- or if you cannot estimate the size you need until runtime. 