# DSA Week 1

## What's an Algorithm?

* A *well defined* a computational process that takes some *input* and produces an *output*.

* Really it's a tool for solving a *well specified* computational problem.

* You don't actually need a computer for them though.

Computation != A Computer.

You can still do this by hand this is called *desk checking*.

## What's a Data Structure?

* A datastructure is just a way to store data

* Really however it is just a special type of algorithm.

## A bunch of this was taught in apps prog.

* All the little patterns taught in App. Prog. are algorithms or templates for algorithms.

* What we're really doing in this subject is starting to build a formal awareness of algorithms as seperate from computer program.

I.e a sum pattern, take a specified input (an array of inputs) and the the output which gives the sum of an array is an algorithm.



## Now Some C++

Now let's explore some of the content for this subject.

* This subject is about DSA, however you'll learn some additional seperate things.
  
  * A noteable example of things learnt include: C++
    
    * The reason C++ is taught, is because it allows a lower access to the computer which allows us to work with datastructures more closely
    
    * We could also do this in python however due to its abstraction it's easy to make things work and if it doesn't work it's hard to debug
    
    * Additionally C++ is one of the most used languages in the world
    
    * This language is heavily used especially if you enter a job which requires low levels
  
  * Another thing learnt is actual algorithms and data structures
  
  * Additionally we're going to learn how to compare algorithms and how to talk about them comparitively. This requires maths however the maths will be overly explored, beyond assestment.
  
  * Additionally we're going to slightly explore algorithmic design paradigms.
    
    * We're going to explore some tools for making algorithms.



## Some Actual C++ (For Real)

### Topics

* Strings (briefly)

* Arrays, or "who thought this was a good idea?"

* Pointers
  
  * References vs Pointers
  
  * Derefencing a pointer

* Classes

* Headers and Source files, or "at least this isn't as bad as arrays"

* Lists & Linked Lists (An actual data structure)



Additionally we may additionally talk about the C++ memory model.



### Strings in C++

Like C# to C++, C++ was how can we improve C and make it object oriented.

* Strings in C are just null terminated **char** arrays
  
  * Aside: ... what is null in C++?
  
  * Mostly just 0, or something that looks like it (yay C)
  
  * Since C++11, an actual *null_ptr* type exists, so you can have a proper null that isn't 0.
    
    * Traditionally old C++, old C++ used to point to the memory pointer of memory 0, which acted like a traditional null pointer exception. Whilst in modern day C++ this points to nothing.
  
  * What could go possibly wrong?
    
    * What if you forget the null?
    
    * What if you want to know the length?
  
  Unlike C, C++ has a proper string class std::string that conceptually wraps a char[] and fixes these problems.
  
  * The :: is called the namespace operator in this case it says in namespace std there is a string. This is similar to C# dot operator i.e std.string.
  
  * In C++ the dot operator still exists however it only applies to getting things from classes i.e string.length
  
  The benefit from C++ is it allows us to wrap code into objects i.e converting a char array into a string class.



All the documentation for the string class and all classes are available online.



### Arrays in C++

If strings are just an array of chars in C++, what is an array in C++?

Arrays in C++ look a lot like Java arrays

* int a[4] = {1, 2, 3, 4}; //Declares size length 4 and statically initalized.

* int a[] = {1, 2, 3, 4}; //Since this is statically initalized we don't need to declare the size it can infer it.

* int a[4] = {};

* int a[4];

These are all statically created? What does this mean?

* Static creations in C++ means something different to what in Java.

### Static & Dynamic Allocation

* C++ has a more complex allocation system than Java (at least from the programmer's perspective)

* Things can be statically allocated:
  
  * They are automatically deallocated when they go out of scope.
  
  * What does this mean for return data?

* Or dynamically allocated:
  
  * Created on the heap with the *new* keyword
  
  * C++ has no garbage collection, so you have to manage it yourself.

In short with C++ don't use *new* unless you have to / mean it.



![Stack & Heap.png](C:\Users\shaan\Documents\GitHub\Data Structures and Algorithms\Week 1\Stack & Heap.png)

I.e a factory method - is a method that creates stuff i.e standardized creation method i.a factory method has things that exist outside of the method so they are not locally on static and have to be created manually i.e on the heap. Whilst java secretly does this in C++ it is known.

* Side Note: When we further explore stack & heap in this course they may not be the same as this definition.
  
  * Additionally their libaries that handle garbage collection and 'smart pointers' i.e pointers that grab the object and when the pointers go out of scope they delete the object & their multiple types of smart pointers.
    
    * I.e smart pointers that delete out of scope.
    
    * Smart pointers that track how many things point to it and when that reaches 0 it does garbage collection
    
    * Pointers that do nothing
  
  * Regardless all of these ultimately end up being done "manually" for a reason. As this is low-level programming for the most case you want to be able to do this.

* Unlike java which allows us to automatically initalize everything, in C++ it doesn't

* In some cases C++ does automatically initalizes things, however in most cases it doesn't automatically initalize anything, it usually *trusts* the programmer thinking you've done this for a reason.



Typically what you have is a hybrid of static & dynamic declorations i.e when creating a datastructure. I.e when creating a datastructure it only needs to exist in a specific scope i.e in a object, so whilst that object exists it stays around. So this avoids the requirement of using "New" as much. And inside the object we have automated methods to clean up the rest of the items inside of the object. Hence we need a thing to delete the object but not everything inside of the object itself.



### Arrays in C++

* In the previous array examples, the sizes were known at decloration

* When you create this array. Memory is statically allocated into the memory and it is set as the array. With this memory allocation we must know how much to allocate, where it asks the operating system asking how much memory in a row to reserve.

* As a result the program does its own memory management - you need to know the size.

* So what happens if you don't know the size or it needs to be dynamic?

* In C++ we literally cannot do this as it can't let us allocate more memory later.

* Arrays decay to pointers to the first element. I.e arrays decay into just a pointer to the first element.
  
  Back to the C++ memory model, we're on the heap which points to an address and once we know the actual size i.e size 5 and the first pointer will point to the memory section of the array. I.e 0xABC pointers to 0xFCM which is the start of the array in memory.
  
  In metaphors its the same as someones home address. The home address tells us where the house is but it is not the house, it just tells us where it is, not giving us the item.
  
  * So an int[] can be treated as an int*.

### Pointers!

* To create a pointer to type *t*:
  
      t * foo;
  
  * The spaces around the * don't matter (i.e t* foo, t *  foo and t *foo are all the same).

* A pointer is really just a number that is the address of whatever it's pointing at.

* To get what it's pointing at we *dereference it* (Derefencing turns the address into the actual value):
  
  * t bar = *foo;
  
  * If you're derefencing to get a member (*foo) .bar, you can write the alternative foo->bar. This can be nicer in many situations as you can chain these which is better then derefencing multiple items.

* To get the address of something, use the address operator:
  
  * int foo = 5;
  
  * int * bar = &foo;

### References

* C++ additionally also has references.

* References are like pointers, however:
  
  * They can't change where they're pointing after initalisation.
  
  * They're transparently dereferenced.

* They're created with the & operator:
  
  * int & foo = ...;

* But then they work like the thing at the other end:
  
  * i.e an int reference works like an int i.e a reference + 5 if the reference is 10 = 15
  
  * To a pointer this will change the memory position
  
  * foo = foo + 5 does what you'd expect (what would it do to a pointer?)

* References are good for passing data around without copying it (this should be familiar from Java - it does essentially the same thing) - Java creates reference types - when you create a thing with new which goes onto the heap it creates a reference / pointer type in Java. Alternatively in C++ we get manual control of this.

### Back To Arrays

* So if we want to create an array where we don't know the size (e.g. as a parameter or return type), we need a pointer:
  
  * int * tabulate(Data dataObject)...

* But how do we know that we're getting an array?

* We don't!

* We.... that's not so good... how do we fix this?

* We use a wrapper, in this case std::vector!

### Classes

* Classes in C++ look a lot like Java classes:

```cpp
#include <string> //This says it's a system library to import
#include "Mem.H" //This imports a non-system library

using std::string; //This allows us to access library functions without actually writing std:: in front of it. NOTE: IT IS NOT ADVISED TO IMPORT NAMESPACE STD AS IT BECOMES AMBIGIOUS

public class myClass : public parentClass //The colon is inheritence
//NOTE: C++ DOES NOT HAVE INTERFACES & THUS ONLY GOES THROUGH INHERITENCE
{
    //We declare members like normal the only issue is that they get          
    //blocked together, order doesn't matter and we can repeat
    private:
    int privateInt;
    
    public:
    int getPrivateInt();
    void setPrivateInt(int newValue);
    string toString();
}; //Additionally we need a semi-colon at the end of a class (For no real reason?!?! It's redundant but it's needed for C++)
```

* Notice that the method have no content here.

* They can but they don't have to

* C++ routinely seperates definitions from source code:
  
  * It expects a single pass compiler, so you have to have all the names in the right order!

* Typically definitions are put in a *header* file (usually .h extension but not necessairly)

* Source code is normally in source files (usually .cpp, but again, that can change).

* Code is put in the header file (sometimes it even makes sense to do so!).

* The convention to use header and source files are entirely semenatic, however it is just best practice to do so. In modern day compilers it does occasionally cause errors.



### Header Files

* So what do we do with header files if they have no code?
  
  * Declare things in the right order for #Includes
  
  * Create the equivilent of interfaces (virtual classes!)



### Some Code

* For this course we're using C++17 Standard, and we're using G++.
  
  * Be careful w/ Microsoft C++ compiler as it uses brasic standard english

```cpp
program.cpp

#include <iostream>
int main()
{
    int a[] = {1, 2};
    
    std::cout << a[0] << ", " << a[1] << std::endl;
    
//If we do a[2] it will give us a huge number, which will give us no answer with no bounds checking or anything.

    //We do get a slightly different thing w/ pointers
    int * a;
    std::cout << a[1] << a[2] << std::endl;
    //We get a segmentation fault (what do you think what happens here), it's not like we can do this to a pointer. What occurs we assign a pointer of a with a ridicioulous amount of memory required (impossible amount) and as such a segfault occurs
    
    int * a = 5;
    //This will give us a conversion warning saying we shouldn't do this
    
    int foo = 5;
    int * a = &foo;
    int ** b = & a; //Nothing special about pointers, we can have a pointer to a pointer i.e a 2D array.
    
    std:: << a << ", " << *a << std::endl;
    //We should get address and the int.
    
    std::cout << b[0] << std::endl;
    
    //For loops look the same
    for(int i = 0; i < 10; i++)
    {
        std::cout << b[i] << std::endl;
    }
}
```






































