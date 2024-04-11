resources: 
	Suggested roadmap: https://neetcode.io/roadmap

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


