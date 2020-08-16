# DSA Week 3

## Content

* Vectors

* Templates

* Iterators

* Big-Oh notation and comparing algorithms

## C++ Vectors

* Arrays in C / C++ are difficult (as we saw), as we cannot dynamically resize them
  
  * No memory protection
  
  * Can resize

* Lists provide an alternative to this but:
  
  * They don't provide the same list of features as arrays does
  
  * won't tell you how the memory is managed
  
  * Lists also comes with more overhead
  
  * I.e getting to the end of a list is slow, getting to an array is very fast

* In C++ Vectors are in the middle ground in terms of arrays and lists.
  
  * If you don't care about how it works, you can just think of vectors as dynamically sized arrays
  
  * Demo: (They're pretty much like arrayLists)
    
    ```cpp
    #include <iostream>
    #include <vector>
    
    public int main()
    {
        std::vector<int> v;
        
        for(int i = 0; i < 10; i++)
        {
            v.push_back(i);
        }
        
        for(int i = 0; i < c.size(); i++)
        {
            std::cout << v[i] << std::endl;
        }
        
        for(int i = 0; I < v.size(); i++)
        {
            v[i]++;
        }
        
        for(int i = 0; i < v.size(); i++)
        {
            std::cout << v[i] << std::endl;
        }
    }
    ```
  
  * Decloration is good
  
  * Adding stuff to the vector is like an arrayList i.e .add is for a vector and for a vector it is push_back()
  
  * Getting it out, as we have a thing called operator overloading, we defined our class to have a square brackets operator

* What are they really? How do they work?
  
  * Look at the documentations on gcc.gru.org
  
  * You legitimately can look at the source code of the vector class in the C++ library (good luck reading it!)
    
    ```cpp
    at - access specified element with bound checking
    operator[] - access specified element
    front - access the first element
    back - acess the last element
    data - direct access to the underlying array
    ```

## Templates

* Templates are like generic types in Java

* As we explored vectors in C++, vectors is a generic / template class. 

* A templated class in C++ is exactly the same as Java, you can give a thing any given type and it will just allocate the memory differently and allow it to work normally. It doesn't change how you access it
  
  * This is beneficial as you can specify an integer, a double a float and the data type without redefining the entire class

* They're fairly simple to work with, but provide lots of places to leave something out (and cause weird compile errors)
  
  * These work weirdly in Java vs C++:
    
    * Java works on compile time
    
    * C++ works on run-time

* One big difference however, is in Java you cannot use primitives, In C++ you can use primitives, additionally if needed you can put actual numbers as datatypes for some reason?
  
  ```cpp
  #include <iostream>
  #include <vector>
  
  int main()
  {
      std::vector<int> v;
      
      for(int i = 0; i < 10; i++)
      {
          v.push_back(i);
          std::cout << v[i] << std::endl;
      }
  }
  ```

* Writing a template. To write a template in C++ you can do

```cpp
template <typename T>
T myMax(T x, T y)
{
    return (x > y) ? true : false;
}
```

## Iterators

* In this week's tutorial you'll see the tail function

* It's a really annoying way to access the list right

```cpp
#ifndef INTLIST_H_
#define INTLIST_H_

class intList
{
    public:
    virtual ~intList() {};
    virtual bool isEmpty() = 0;
    virtual void prepend(int c) = 0;
    virtual void append(int c) = 0;
    virtual int getList() = 0;
    virtual intList * tail() = 0;
}

#endif
```

* To move along this list you continously get the tail until it is empty which is quite annoying

* What we would like is a simple way to get to the next element, that's still compatiable with the information hiding.
  
  * Instead of doing something like this we want a more simpler more robust way of accessing our list like our vector.
  
  * In our vector it is good, however in some data structures it's not really well defined, as well as the end of the list not being well defined. I.e a circular queue is not really well defined for the start / end
  
  * What we want would like a simple generic way to get the next element, that's still compatiable w/ information hiding

* Iterator is the answer to this problem

* Iterators in Java are fairly well put together:
  
  * The inheritance structure is well thought out so it works well and everything has to extends iterable.
  
  * I.e for-each loop in java
    
    ```java
    for(int i : v)
    {
        
    }
    ```

* As you expect, C++ can do the same thing, but you pay for it with some more ugly Code:

### Inheritance In Java Vs. C++

#### Java

* In Java we do dynamic late dispatching

* So if we have a parent class A and a sub-class B and

* class B extends A

* If we do: A a = new B() and they both have a .size() method which one runs if we do a.size()?
  
  * We run the B definition so we actually convert the A object to a B variable

#### C++

* In C++ we can do the same thing. Class B extends A

* Class B = public A

* C++ does early dispatching as such as we get class B in this case, UNLESS we denote the method as a **virtual**

## 

## Algorithm Analysis

### Analysing and Comparing Algorithms: Big-Oh Notation

* Like lets say who makes the best algorithm for one problem:
  
  * Speed
  
  * How much memory does it use
  
  * How much lines of code
  
  * Readability
  
  * Useability

* How do we reliably compare algorithms?
  
  * Testing gives good information, but is limited to the test cases you test.
  
  * How fast it when you don't have time to do testcases & you're working on industry
  
  * How much of that information comes from the choice of, computer, programming languages, test data?
  
  * So in terms of testing algorithms there's all these cofounding factors so how do we compare the speed of the actual algorithm itself, regardless of setup, language test data etc.
  
  * Thus we need a way of testing the abstract algorithm itself. If we have two algorithms that solve the same problem, what things are we interested in?
    
    * How fast are they
    
    * How much space do they take up

* How do we know what resources an algorithm will use for an infinite number of inputs

#### A Diversion into Mathematics

* For solving these issues we jump back into the foundation of mathematics. At a fundamental level computers are just mathematical objects, as such we can model this in maths

* If we have two functions *f* and *g*, we have a way of comparing them:

![](C:\Users\shaan\AppData\Roaming\marktext\images\2020-08-16-13-45-16-image.png)

* Constant c and Constant N

* f(n) <= c * g(n)

* Or: for big enough numbers, f(n) is less than or equal to a constant times g(n)

* Q is rational numbers

* N is natural numbers (>= 0 integers)

![](C:\Users\shaan\AppData\Roaming\marktext\images\2020-08-16-13-54-33-image.png)

* After the startpoint point c * g and g binds how fast f is

* As such c * g is an upper bound limit

* But after our starting point g and our constant c bounds our starting points.

* The graph he shows that f <= c * g
  
  * And if this is true forwever, then eventually g will overtake f or be the same

* Big o is the g value where f is faster.

* What makes this interesting is what we label our y-axis as:
  
  * Time complexity
  
  * memory
  
  * threads

![](C:\Users\shaan\AppData\Roaming\marktext\images\2020-08-16-13-48-49-image.png)

#### Some Examples

![](C:\Users\shaan\AppData\Roaming\marktext\images\2020-08-16-14-08-00-image.png)

1. If f(n) = n and g(n) = 2n this implies our f is of O(g)

2. If f(n) = n, g(n) = n^2 implies f is of O(g)

3. For question (4) you can change the constant to C = 1/50 to make this work

![](C:\Users\shaan\AppData\Roaming\marktext\images\2020-08-16-14-14-26-image.png)

* In a nutshell, big O is just about growth rates

* How do you do big O analysis if it's hard to quantize the input? In computational it is generally easy to quantify the input

#### Proving These Relationships

* These can be provided by a variety of techniques:
  
  * Induction
  
  * Algebracially
  
  * Limit based definitions

* We'll leave proofs for now but there's a bunch of handy rules:

![](C:\Users\shaan\AppData\Roaming\marktext\images\2020-08-16-14-18-49-image.png)

* If you're function consists of lots of functions added together, you take the worst function as your big O function

#### For the more mathematically inclined...

![](C:\Users\shaan\AppData\Roaming\marktext\images\2020-08-16-14-20-53-image.png)

* Use L'Hopitals rule

#### Some handy names

* n is linear

* n^2 is quadratic

* n^3 is cubic

* n^k is polynomial

* log(n) is logarithmics

* (log(n))^k is poly-logarithmic

* k^n for any k is exponential

 

#### How does this help us?

* Back to two algorithms A and B:
  
  * If we can work out functions that describe running time, we can compare them and decide what is fastest (in the long run)
  
  * So if we can make up functions to describe it we can compare which one is fastest

* Working out:

![](C:\Users\shaan\AppData\Roaming\marktext\images\2020-08-16-17-53-49-image.png)

(Because A's running time is always bigger then B for a large enough number)

#### Algorithmn Analysis

* How do we get a function then?

* In an abstract sense, running time is really the number of steps the algorithm takes for a given input size:
  
  * This abstracts out programming languages and computers

* So "all" we need to do is count the number of steps.

```markdown
begin
    a = 1
    b = 2
    c = a + b
    
    print c
    
end
```

This code does the same thing for any "input" (it doesn't really take any), So T(n) = 4 (ish)

* It's ish since print may be multiple steps

* Addition plus assignment may be multiple steps

* Since it's not in a specific language the complexity can be questionable

* In conclusion this doesn't really matter, if the input is changed it doesn't really change how long it takes to run

* This program is trivial as it's a constant time program

```cpp
void printArray(int a[], size n)
{
    for(int i = 0; i < n; i++)
    {
        std::cout << a[i];
    }
}
```

* At each iteration we do a check to see if i is large enough to stop, print something out and add one to i. We also initalise i once.

* Assume printing is one step

* T(n) = 1 + 3n is in O(n)
  
  * Printing to cout is one operation
  
  * i++ is one thing
  
  * checking if I is large enough to stop
  
  * Additionally we also declare int i ONCE



```cpp
for(int i = 0; i < n; i++)
{
    for(int j = 0; j < n; j++)
    {
        System.out.println(i + " " + j);
    }
}
```

* For each iteration of the outer loop, we have n iterations of the inner loop, we do one thing. So if the outer loop runs n times:
  
  * T(n) = n * n * 1 = n^2 in O(n^2)



My Theory:

* We do one loop, we initalize i = 0 and check if i < n

* We additionally do this another time with j = 0 and check if j < n

* We print out the line

So like 6n^2 + n + 2



Answer:

* We only take the worst O(n) time complexity value

* Additionally as 6 is a constant that is turned into the 'c' and is therefore removed (somehow) ask for clarification / study discrete.

#### Some other properties and notations

![](C:\Users\shaan\AppData\Roaming\marktext\images\2020-08-16-18-24-50-image.png)


