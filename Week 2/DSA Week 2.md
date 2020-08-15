# DSA Week 2

In week 1 content we said we ran out of time to cover LinkedLists and as such we will cover them now.

So you may remember from the end of the last lecture we talked about the file structure of the C++ program, where we have header files & source files.

In this week we will cover our first data structure in the context of how that would be built in C++. Their will be a lot of content that wont quite make sense yet but will be further explored next week.

As mentioned there is a thing called header files, usually the extension .h

```cpp
#ifndef INTLINKEDLIST_H_
#define INTLINKEDLIST_H_

#include <cstddef>
#include <string>

#include "intList.h"

using std::string_t;
using std::string;

class intLinkedList : public intList
{
    private:
    class intNode
    {
        private:
        intNode * next;
        int data;

        public:
        intNode();
        intNode(intNode * next, int data);
        ~intNode();
        int getData()
        intNode * getNext();
        void setNext(intNode *);
    };

    intNode * head;
    size_t length;
    
    public:
    intLinkedList();
    ~intLinkedList();
    bool isEmpty();
    void prepend(int c);
    void append(int c);
    int getHead();
    intLinkedList * tail();
};

#endif
```

The intNode class is a class which has a pointer to the next node and and int to store the data. Additionally the Node class has two constructors (overloading) as well as a destructor ~intNode().

As explained before C++ does things manually, if you create something on heap, you additionally have to remove it yourself through a destructor. This isn't really needed if the object is put on the stack, however you can make it do non-memory realted tasks when it's done.

Additionally it's got public methods to access private data, through good OOP practices.

The LinkedList is a prime example of where pointers would be used.

When ending a class we need a semi-colin;

The intLinkedList class is another class w/ constructor, destructor, bool isEmpty, a method to add to start of list, method to add to end of list, method to get the front of the list and method to get the end of the list.

 #include is similar to the import keyword in Java.

To make these imports work we use the c-standard defined library, in these libaries we are using string as well as size_t

The using keyword allows us to write std::size_t as size_t (Usually the using keyword shouldn't be used as it can be ambigious especially with similar structure files)

For importing libraries if it's in the C standard library we use <> otherwise if it's a usermade class we use double quotes.

## C++ and Types

* With java we had a limited number of primitive types, float, double, boolean, char, long etc.. and we had a bunch of our own objects which were their own types.

* C++ has many more things which aren't objects which are types.

I.e when intLinkedList is created it becomes a type. But in the same way we have int, we have many more primitives such as size_t.

The things prying into this is C++ uses types to define roles. Underneath beneath all of this size_t is an unsigned int that holds a positive value. By using size_t it tells us that it's supposed to hold the length of something.

The second thing playing into this is we can also define types into C++, through this we can do weird operations such as relabel one type as another i.e longnamespaces can be relabeled into something shorter.

One additional header piece of information.

```cpp
#ifndef INTLINKEDLIST_H_ //If not defined
#define INTLINKEDLIST_H_ //If defined

#include <cstdlib>

#endif
```

These are called compiler directives, the most useful one is the include keyword, the rest whilst not really needed can be used to make the compiler do complicated things outside the scope of this course.

Since C++ is a single run compiler we need to include it in the top before using it in the bottom. In effect we need to define our functions files in the top.

As such we don't want to include the definition twice however we want at least one references at the top. As such this is what the catch does on top. the ifndef and define. If not defined do this or else we do the other thing.

Pretty much this is a glorified if statement for the compiler. This acts a guard which if the code doesn't exist create it otherwise skip it. Additionally we can have code below it. An error of this is using a label that already exists such as importing string from cstdlib and defining the header as string.

Next is inheritence of linkedLists.

* An interface in java is an alternative inheritance mechanism, where we say if class a implements class b. B says A must have these parameters.

Interesting enough C++ only does inheritence i.e extends however we can manipulate it to work as an interface.

```cpp
#ifndef INTLIST_H_
#define INTLIST_H_

    class intList
    {
        public:
            virtual ~intList() = 0;
            virtual bool isEmpty() = 0;
            virtual void prepend(int c) = 0;
            virtual void append(int c) = 0;
            virtual int getHead() = 0;
            virtual intList * tail() = 0;
    }

#endif
```

So through this "interface" we can see we have the keyword virtual and the 0. These are called "Pure" virtual functions with the value of 0.

The way C++ inheritence works is without the virtual and the = 0 and we had a file that inheritented the int list it would run this method, the one which is defined in here, which is different to what java does. 

In java uses dynamic late b: i.e A extends B and create a variable type B and extends B and we use the method getHead on B it will get the one from A.

C++ will instead get the one closest to the starting point.

What the virtual keypoint does is forces it down, making it lower in the hierarchy. The = 0 says it has no instanceuation. So then it will run not use the virtual method however if it can't find one it will be used later.

This allows us to pretty much make our own version of java interfaces.

However what's the point of using a header file and C++ file. This is the same polymorphism argument used in Java. Usually we dont' care if it's linkedlist an arrayList etc. usually we care about it being a list. i.e The List of Substitution Principle.

So what it gives us is a way to say that the thing is not really in intList but we just really want a List. and hence a bunch of different programmers could make their own implementation of linkedList and we should be able to substitute them without changing our code in runtime - This is just an OOP principle not just C++.

So a list in an extent is a natural extension of an array.

![](C:\Users\shaan\AppData\Roaming\marktext\images\2020-07-18-18-34-45-image.png)

An array is our classic ORDERED data structure. 

* Array
  
  * Ordered
  * Fixed sized

Additionally these are all in one blocks in memory - so this allows us to optimize memory operations.

However, in practice we don't always have the other thing in lists, that is arrays are FIXED in size.

What happens however if we only want the ordered part? Where we don't want the fixed size?

* This is where lists come in.

* A list is a bunch of things in order with no other particular constraints.

This is our first data structure: A list is an ordered data structure

![](C:\Users\shaan\AppData\Roaming\marktext\images\2020-07-18-18-37-13-image.png)

It does not say anything about the size, anything about it being stored in memory, how they're connected together etc..

A list is a thing that implements these methods

* We can tell if empty

* We can add something to the front of it

* We can add something to the end of it

* We can get the front of it

* We can get everything but the front of it
  
  * This in turn gives us a primitive way of iterating

A linked list is a type of list that then uses pointers or something like pointers to link each other into a specified order.

* You can think of a linked list being a collection of nodes with data and the pointer to the next Node.

* The first Node is called the head

* The last Node is called the tail

As these nodes need to be dynamically allocated it means these must be created on the heap as we DO NOT WANT THESE TO BE STATICALLY CREATED. Otherwise they get destroyed. This means we're forced into using the **new** keyword as well as using **destructors**.

From C++ inheriteted in C is a ****struct****, which is like a class but everything is **public**.

As we said previously, this is a header file. As such it contains all the definition but no content, so where do we put the content?

We put it back in our .cpp file (the source file)

We include the headerfile so we know what it's supposed to be and we implement it with the double operator colon.

```cpp
#include "intLinkedList.h"

intLinkedList::intNode::intNode()
{

}

intLinkedList::intNode::intNode(intNode * n, int d)
{

}

intLinkedList::intNode:~intNode()
{
    //You don't have to do anything for this one
}
```

and with these we fill in the methods for the implementation.

* The type and additional information for implementation method is not listed in the .cpp file. This is because all of this information is done and implemented in the header file. As such it is different from a java program where there combined.

## This Weeks Content

* Simple I/O

* Classes & importance of destructors

* Exceptions

* Compilation w/ multiple files

* Data Structures:
  
  * Queues
  
  * Stacks

### CIN and COUT

* As with everything C++ has a number of ways to handle basic text input and output

* In this lecture we will be going through cin and cout which is the more or less "basic way" to handle inputs and outputs in c++

* COUT and CIN are the standard operators
  
  * They work in the same way as Java's system.in and system.out
  
  * But they come with special operators: >> and <<

* They are in the iostream library in the C++ standard library

* Write to standard output with
  
  ```cpp
  std::cout << "Stuff to write";
  ```
  
  * To output multiple things we can chain the <<
  
  * This << is a stream operator (similar to javas streams). C++ handle streams with this symbol (also bitshift operator)

* They are in the iostream library in the standard C++ Standard library

* Reading in with
  
  ```cpp
  std::cin >> "destination";
  ```
  
  * CIN has a unique property where it stops at the first whitespace character " "
  
  * To read in a whole line cin won't cut it, instead use:
    
    ```cpp
    getline(cin, "variable to read into");
    ```

* cerr also exists for errors (equivalent to system.err in java)

### And now a demo!

```cpp
#include <iostream>
#include <string>

int main()
{
    std::cout << "Hi" << 1 << << std::endl; //To append stuff you need to use the string operator
    
//Takes in user input as a string
    std::string s;
    std::cin >> s; //This one only works for a string w/ no spaces
    
    getline(std::cin, s);
    
    std::cout << s << std::endl;
}
```

* As getline is not a class or anything, just a function from the <iostream> library it does not require you to specify std:: infront of it, instead you can just use it.

## File I/O

* Uses the same abstractions as cin and cout, but with a little more fiddling

* * Uses the library fstream
  
  * Create an ofstream for writing
  
  * Creates an ifstream for reading

## Classes & Destructors

* You may have noticed a weirdly named function last week:
  
  ~intLinkedList();

* This is a *destructor*

* This is a special method that runs when an object has a special delete operator called on it.
  
  * Syntax:  delete [pointer to the thing to delete]
  
  * For arrays: delete[] [array variable]

#### Why do we delete things?

* delete is needed when we've created something with "new".
  
  * This is required otherwise you're program is fucked

* I.e we need to setup a method to delete the object when the lifetime of the object ends

* Otherwise the heap memory is not deallocated, and we have a memory leak. (This can crash your computer)

* The programmer has to choose when to do this (so again, don't use new unless you mean it).

### Exceptions

* C++ can throw exceptions, just like Java

* Exceptions are there for when something in Java

* Exceptions should not be used as a flow of control as they are incredibly resource heavy,
  
  * A good version of this is i.e string input and you want an number
  
  * Throw a number format exception
  
  * Catch exception (loop, actually put a number not a string) (User exception)
  
  * The nicer way of doing this is to just sanitize input and avoid the exception

```cpp
try{
    
}
catch([Exception Type])
{
    
}
```

* The fun part is.. C++ can throw *anything!*

* Java has a strict hierarchy that everything inherits from and everything is nice and coherient and you can treat everything as objects (excluding primitives)
  
  * C++ does not have this i.e voids it's just bits and pieces over time
  
  * This means C++ does not have a central exception hierarchy that java does. I.e java has java.runtime.throwable, error, runtimeexception and exception
  
  * When java gets an error the program should stop, when a runtime exception occurs the program will stop but be able to tell the user, or a plain exception can be recovered from
  
  * C++ doesn't have anything like that, it just throws stuff

```cpp
#include <iostream>
#include <string>

int main()
{
    try
    {
        int c;
        std::cin >> c;
        bool b = true;
        throw 1.0;
#       throw b;
#       throw c;
    }
    catch(int i)
    {
        std::cout << i << std::endl;
    }
    catch(bool b)
    {
        std::cout << b << std::endl;
    }
}
```

* This block of code should be able to throw an integer and echo an input

* We can additionally do catch overloading / choosing the most appropiate one.

* If we throw something that isn't caught we get a "core dump" error. I.e throwing a decimal when we only have an int or bool.

* Having said that C++ does have a small set of exceptions and you can somewhat mimic java.



* Note: The int for main refers to error codes; 0 refers to no errors, and changing the value depend on an error table.

## Data Structures

### Queues

* The (basic) Queue is the basic FIFO (first-in-first-out) data structure

* It keeps things in order like a list, however you can only add things in the back, but things can only be taken off from the front.

* Additionally w/ more advanced versions of queues (i.e priotity queue makes it more complex)

* Normally it has an unbound capacity (though there is a technical limit)

#### A Pure-ish Virtual class for a queue of ints

```cpp
class intQueue
{
    public:
    virtual ~intQueue() {}
    virtual void enqueue(int n) = 0;
    virtual int dequeue() = 0;
    virtual int peek() = 0;
}
```

* Has an enqueue (adds to the back)

* Take something from the queue from the front

* Peek function (look at front but not take it off)

![](C:\Users\shaan\AppData\Roaming\marktext\images\2020-08-15-19-00-17-image.png)

* Note this is not an implementation, this is an header. So this is a piece of code that represents an **abstract data structure**
  
  * An abstract datastructure is a collection of behaviours

#### Other types of queue

* A **dequeue**: is a double-ended queue - you can add and remove for both ends!
  
  * This is really useful to implement other data structures

* A **priority queue**: is a queue, but elements are inserted in priority, and come out in the priority order.

### Stack

* A stack is like a queue, but it's a last-in-first-out (LIFO) data structure
  
  * It's like a ... stack of things

* Whenever you put in most recently is the first thing to come out

* You can add to the "top of it" and only remove the top one (like you can't really remove the middle or bottom of it)

#### A pure virtual class for a stack of ints

```cpp
class intStack
{
    public:
    virtual ~intStack() {};
    virtual void push() = 0;
    virtual int pop() = 0;
    virtual int peek() = 0;
}
```

### Stacks & Queues

* Stacks and Queues are the two most used datastructures that actually "do" something

* Buffers of all kinds are Queues (things go in, and get processed in order eventually)

* Stacks are build in programming languages you're using - they control how the program functions

* You'll see more of them in upcoming lectures


