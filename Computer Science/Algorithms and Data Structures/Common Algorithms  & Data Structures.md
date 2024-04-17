resources: 
	Suggested roadmap: https://neetcode.io/roadmap

### basic algos
- histogram - for a fixed dataset size (ten for example) you create an array of that dataset size or possible responses and you record in the index of the array everytime that number is encountered in the data set to count how often a number is recorded. useful for findind the mode. and then run through each index of the recording array to see which one has the biggest value. time complexity of O(n) scales linier to the dataset
### sorting algos
- qsort(c++)
	- struggles where there are duplicate values and will take longer. works well with smaller sets though.

### Data structures

Linked List: 
```cpp
```
###### Middle of the Linked list: 
for this one you need to do a fast pointer that moves through twice the amount of nodes as a slow pointer
```javascript
fastPtr = head;
slowPtr = head;

while(fastPtr !== null){
	fastPtr = fastPtr.next.next;
	slowPtr = slowPtr.next;
}
```

#### Graphs
edges 
vertices
#### Stacking
enqueue
dequeue
with array/linked lists
#### Hashmap/Hashing
- involves the combination of an indexed array called a hash table that uses a function called hash function to return a index to store the node or value at. 
- collision will happen if you have more than one value that will hash to the same index (i.e apple in index 0 and ant also hashes to the index 0)
	- the solution to these collisions are two: 
		- linear probing: when you find the next available index in the array
			- not great becuase it starts clustering which is when too many values or keys are hashing the same index and accumulating along the index length which could devolve the speed of look up to linear o(n)
		- Seperate chaning: when you create linked lists at the key location to allow items to chan together in either a single or doubly linked list.
###### growth of a hash table
- most languages start at 16 because its a power of 2 but it could depend on your use case. 
- what happens when you hash an input into a bigger number than you have indexes?
	- use the modulo operator by the number of indexes you have and it will return a number between 0 and the number of indexes you have minus one. 1084 % 16 = 
- Eventually though we will have too many nodes for the amount of buckets so it will need to be doubled in size and all the nodes copied over to the new table
	- how to know when you grow: 
		- capacity- the number of buckets you currently have
		- factor- determines at which point it will add more. expressed as a number between 0-1 e.g .75. usually it is between .75 and 1 accross implementatoins
###### choosing a good hash function
- what do we want to consider for choosing a hash function?
	- avoid collisions as much as possible by distributing keys as evenly across the table as possible (avoid something like taking first three digits of phone number that thousands of people are going to have in common. better the last three digits)
	- it should be simple and easy to compute

#### Binary Tree
##### recursion and binary tree
##### in order
##### preorder




#### Heap
##### max heap
##### min heap
