priority: 
- Rational
- Vector class

Vector class notes
- operator overloading for copy =
- append operator >> 

Iterator notes: 
- its a class that can act like a pointer 
- Iterator it = list.find(23);
- list.remove(it);
- delete it // syntax error

nested classes 
class 
	- define another class insdide of it

```cpp
stack<inst>::ITerator it;

```
- `friend class List` - inside the public section of the class 


##### inheritance
- a pointer of the parent class can be assigned to the parent class or any of the children that inherit from parent class. 
- for sfml bouncing shapes we will have vector of multple classes of shapes


##### SFML Notes
graphinc calculator
- challenges: sdrawing -5 in sfml 
- post fix your expression from the tree to get token order
- youre going to use a stack to handle tokens objects to handle operators and operands. if you seef(x) = 2 cos2(x),      a = 0
	- each token is an object, struct of somekind
- operand push to stack, if you see operator, you pop to get the two oerands and handle the operation on them
	- i. e `(3+5)*8 3 5 + 8 * `
	- use iterator for popping queue and other structure traversal
	- evaluation method is called rpn revers polish notaiton evaluation method
- shunting yard algorithim is what allows for the organizing infix expressions into postfix expressions. refer to the wikipedia for more information
	- it uses a stack and a queue
	- number in the queue
	- operator goes in the stack

