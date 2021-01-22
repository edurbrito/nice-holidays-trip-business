# Object Oriented Programming 
Definition:
```
    Object-oriented programming (OOP) is a 
    programming paradigm based upon objects
    (having both data and methods) that aims 
    to incorporate the advantages of modularity
    and reusability.
```

#### Overview Considerations:
* Each Object includes its own copy of the _data members_(local state variables viewed as attributes)
* Class methos are applicable to objects of the class
* keyword `public` marks the beginning of each public section
* keyword `private` marks the beginning of each private section - variables and functions in here can only be invoked and accessed inside methods of the same class
* normally,the data members are placed in private section(s) and the function members in public section(s)
* Constructor: special function that is a member of the class and has the same name as the class; does not have a return type and is automatically called when an object of that class is created
* `const` member functions can't modify the object that invokes it (`intgetNumerator() const;` for example) 
  * Note: See <https://stackoverflow.com/a/36815110> for difference between static and const (static here means only one copy for all objects, they are defined outside the class body)
* `this->` pointer. See <https://www.geeksforgeeks.org/this-pointer-in-c/>
----
#### Separate compilation:
###### Header Files:
Files that define types or functions that are needed in other files, are a path of communication between the code and contain:
* The complete interface of the class
* Its declaration
* definitions of constants
* definitions of types / classes
* declarations of non-member functions
* declarations of global variables

Note: The `#ifndef` directive can be used to prevent  multiple declarations of a class For example

```
#ifndef BOOK_H
#define BOOK_H
// the Book class definition goes here
#endif
```

###### Cpp Files:
May contain:
* definitions of member functions
* definitions of nonmember functions
* definitions of global variables

---- 

#### Class Destructors:
The name of a destructor is a `~Name_of_the_Class`:
* A destructor is a member function of a class that is called automatically when an object of the class goes out of scope
* This means that if an object of the class type is a local variable for a function, then the destructor is automatically called as the last action before the function call ends
* Destructors are used to eliminate any dynamic variables that have been created by the object, so that the memory occupied by these dynamic variables is returned to the freestore
* Destructors may perform other cleanup tasks as well

#### Templates:
`template<typenameT>` Is the common implementation for templates. See the full explain here <http://www.cplusplus.com/doc/oldtutorial/templates/>

#### STL Containers:
Data structures capable of storing objects of almost any data type.
There are 3 styles of containers:
* first-class containers
* adapters
* near containers

###### First class containers:
* Sequence containers:
represent linear data structures, such as vectors and linked lists
  * vector
  * deque
  * list
  * NOTE: string -supports the same functionality as a sequence container, but stores only character data
  
    Deque and vector provide random access, list provides only linear accesses. So if you need to be able to do *container[i]*, that rules out list. On the other hand, you can insert and remove items anywhere in a list efficiently, and operations in the middle of vector and deque are slow.
    Deque and vector are very similar, and are basically interchangeable for most purposes. There are only two differences worth mentioning. First, vector can only efficiently add new items at the end, while deque can add items at either end efficiently. So why would you ever use a vector then? Unlike deque, vector guarantee that all items will be stored in contiguous memory locations, which makes iterating through them faster in some situations.
    Use deque if you need efficient insertion/removal at the beginning and end of the sequence and random access; use list if you need efficient insertion anywhere, at the sacrifice of random access. Iterators and references to list elements are very stable under almost any mutation of the container, while deque has very peculiar iterator and reference invalidation rules (so check them out carefully).
    Also, list is a node-based container, while a deque uses chunks of contiguous memory, so memory locality may have performance effects that cannot be captured by asymptotic complexity estimates.
    Deque can serve as a replacement for vector almost everywhere and should probably have been considered the "default" container in C++ (on account of its more flexible memory requirements); the only reason to prefer vector is when you must have a guaranteed contiguous memory layout of your sequence.

* Associative containers
nonlinear containers that typically can locate elements quickly; can store sets of values or key -value pairs
  * set
  * multiset
  * map
  * multimap
    In simple words, set is a container that stores sorted and unique elements. If unordered is added means elements are not sorted. If multiset is added means duplicate elements storage is allowed.
    A std::map is an associative container, that allows you to have a unique key associated with your type value.
    A std::multimap is equal to a std::map, but your keys are not unique anymore. Therefore you can find a range of items instead of just find one unique item.
    The std::set is like an std::map, but it is not storing a key associated to a value. It stores only the key type, and assures you that it is unique within the set.
    You also have the std::multiset, that follows the same pattern.

###### Container adapters: 
* stack
* queue
* priority-queue

###### Near containers(non-STL, but with STL-like characteristics and behaviors):
* bitsets
* valarrays
* strings
* C-like pointer-based arrays

###### New C++11 containers:
* Sequence containers:
  * array
  * forward_list
* Unordered associative containers:
  * unordered_set
  * unordered_multiset
  * unordered_map
  * unordered_multimap

#### STL Iterators:
Used by programs to manipulate the STL container elements, have properties similar to those of pointers and there are 5 categories.

`*it`-dereferences iterator `it`
  * `it++` -moves it to the next element of the container
  * other available operators: --, ==, !=(<, <=, > or >= only for random-access iterators)
* container member-functions
  * `begin()` –returns an iterator located at the 1st element in the container
  * `end()` –returns an iterator located one beyond the last element in the container
* Basic outline of how an iterator can cycle through all elements of a container:
```
STL_container<type>::iterator p;
    for (p = container.begin(); p != container.end(); p++) 
        process_element_at_location p;
Ex:
vector<int> v1; 
// FILL v1 WITH SOME VALUES ...
vector<int>::iterator p;
for (p = v1.begin(); p !=v1.end(); p++)
    cout << *p << endl;// ... AND SHOW THE VALUES
```
The iterator category that each container supports determines whether the container can be used with specific algorithms in the STL.

* Constant iterators:
    * a constant iterator is an iterator that does not allow you to change the element at its location
* Reverse iterators
  * a reverse iterator is an iterator that can be used to cycle through all elements of a container,in reverse order,provided that the container has bidirectional iterators;
  * basic outline of how a reverse iterator can cycle through all elements of a container:
  ```
  STL_container<type>::reverse_iterator p;
  for (p = container.rbegin(); p != container.rend();p++)
    process_element_at_location p;
  Ex:
  vector<int> v1;
  // FILL v1 WITH SOME VALUES ...
  vector<int>::reverse_iterator p;
  for (p = v1.rbegin(); p != v1.rend(); p++)
    cout << *p << endl; // ... AND SHOW THE VALUES
  ```
  * `rbegin()` – member-function that returns an iterator located at the last element
  * `rend()` – member-function that returns a sentinel that marks the "end" of the elements in reverse order
  * note that for a reverse_iterator, the increment operator, ++,moves backward through the elements
* Iterators and element insertion/removal
  * note that when you insert or remove an element into or from a container, that can affect the other iterators
  * in general, there is no guarantee that the iterators will be located at the same element after an addition or deletion
  * some containers do, however, guarantee that the iterators will not be moved by additions or deletions, except if the iterator is located at an element that is removed(ex: list; vector and deque make no such guarantee)

###### NOTE: Iterators in C++11
In C++11, the `auto` keyword makes this a little easier:
```
for(auto vPtr = v.begin(); vPtr != v.end(); vPtr++)
    cout << *vPtr << endl;
```
###### Range-based for() loops
An even simpler syntax to allow us to iterate through sequences, called a range-based for statement(or “for each”):
```
for(auto x: v) //OR   for (const auto &x: v)=>x can't be modified
    cout << x << endl;
```
You can translate this as “for each value of x in v”.
If you want to modify the value of x, you can make x a reference
```
for(auto &x: v) // x can modified
    x = 10 * x;
```
This syntax works for C-style arrays and anything that supports an iterator via begin() and end() functions. This includes all standard template library container classes (including string).

-----
###### Summary:
* STL - a library of classes that represent containers that occur frequently in computer programs in all application areas.
* Each class in the STL supports a relatively small set of operations. Basic functionality is extended through the use of generic algorithms. 
* The 3 fundamental data structuresare the vector, list, and deque. 
* Vector and deque are indexed data structures; they support efficient access to each element based on an integer key. 
* A list supports efficient insertion into or removal from the middle of a collection. Lists can also be merged with other lists.
* A set maintains elements in order. Permits very efficient insertion, removal, and testing of elements. 
* A map is a keyed container. Entries in a map are accessed through a key, which can be any ordered data type. Associated with each key is a value. A multimap allows more than one value to be associated with a key. 
* Stacks, queues, and priority queues are adapters built on top of the fundamental collections. A stack enforces the LIFO protocol, while the queue uses FIFO. 
-----



#### Algorithms:
“Generic Algorithms” are template functions that use iterators as template parameters.

NOTE: 
* Algorithms act on container elements; they don't act on containers
* parameters are iterators not containers
* the container properties (ex:size) remain the same

* Nonmodifying algorithms:
    Algorithms that do not modify the container they operate upon.
    * find - locates an element within a sequence.
      *   `Iter find(Iter first, Iter last, const T&value);`
    * count - counts occurrences of a value in a sequence
    * equal - asks:are elements in two ranges equal ?
    * search - looks for the first occurrence of a match sequence within another sequence
    * binary_search - searches for a value in a sorted container. This is an efficient search for sorted sequences with random access iterators

* Modifying algorithms:
  Container modifying algorithms change the content of the elements or their order.
  * copy - copies from a source range to a destination range; this can be used to shift elements in a container to the left provided that the first element in the source range is not contained in the destination range. 
  * remove - removes all elements from a range equal to the given value. Must be followed by erase()
  * random_shuffle - shuffles the elements of a sequence.
  
* Sorting algorithms
  * sort - sorts elements in a range in nondescending order, or in an order determined by a user-specified binary predicate. 
  * merge - merges two sorted source ranges into a single destination range.

* Numeric algorithms
  * accumulate - sums the elements in a container.

