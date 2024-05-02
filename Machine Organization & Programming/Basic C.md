#C #Pointers #CS354 #UWMadison

```C
int* varname; // Creates a pointer
```

[[Memory Hierarchy]]
Order of virtual address spaces from low to high:
Code
Data
Heap
Stack

### Structs
When given a ptr to a struct, you must access fields like:
ptr-->field
or \*(ptr).field as \*ptr.field does not work. 
Structs can be nested in structs

### Various C
sbrk()
- changes the top of the heap by a user given number of bytes