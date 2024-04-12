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

#### Binary Tree
##### recursion and binary tree
##### in order
##### preorder




#### Heap
##### max heap
##### min heap
