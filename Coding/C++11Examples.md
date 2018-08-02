# C++11 Examples
- [C++11 Examples](#c11-examples)
    - [C++ STL](#c-stl)
        - [\<list\>](#list)
            - [std::list](#stdlist)
        - [\<vector\>](#vector)
            - [std::vector](#stdvector)
        - [\<functional\>](#functional)
            - [std::function](#stdfunction)
        - [\<utility>](#utility)
            - [std::pair](#stdpair)
            - [std::move](#stdmove)
            - [std::forword](#stdforword)
    - [Key Words and Operator](#key-words-and-operator)
        - [auto](#auto)
        - [explicit](#explicit)
        - [& and &&](#and)
        - [lambda expression](#lambda-expression)
        - [constructor and deconstructor](#constructor-and-deconstructor)
        - [delete and default](#delete-and-default)
    - [boost](#boost)
        - [optional](#optional)

## C++ STL

### \<list\>

#### std::list

Constructs a list container object, initializing its contents depending on the constructor version used:
1. empty container constructor (default constructor)
Constructs an empty container, with no elements.
2. fill constructor
Constructs a container with n elements. Each element is a copy of val (if provided).
3. range constructor
Constructs a container with as many elements as the range [first,last), with each element emplace-constructed from its corresponding element in that range, in the same order.
4. copy constructor (and copying with allocator)
Constructs a container with a copy of each of the elements in x, in the same order.
5. move constructor (and moving with allocator)
Constructs a container that acquires the elements of x.
If alloc is specified and is different from x's allocator, the elements are moved. Otherwise, no elements are constructed (their ownership is directly transferred).
x is left in an unspecified but valid state.
6. initializer list constructor
Constructs a container with a copy of each of the elements in il, in the same order.

```C++
#include <iostream>
#include <list>
#include <iterator>
 
 
int main()
{
	std::list<int> listOfNumbers;
 
	//Inserting elements at end in list
	listOfNumbers.push_back(5);
	listOfNumbers.push_back(6);
 
	//Inserting elements at front in list
	listOfNumbers.push_front(2);
	listOfNumbers.push_front(1);
 
	// Iterating over list elements and display them
	std::list<int>::iterator it = listOfNumbers.begin();
	while(it != listOfNumbers.end())
	{
		std::cout<<(*it)<<"  ";
		it++;
	}
	std::cout<<std::endl;
 
 
	//Inserting elements in between the list using
	// insert(pos,elem) member function. Let's iterate to
	// 3rd position
	it = listOfNumbers.begin();
	it++;
	it++;
	// Iterator 'it' is at 3rd position.
	listOfNumbers.insert(it, 4);
 
 
	// Iterating over list elements and display them
	it = listOfNumbers.begin();
	while(it != listOfNumbers.end())
	{
		std::cout<<(*it)<<"  ";
		it++;
	}
	std::cout<<std::endl;
 
 
	//Erasing elements in between the list using
	// erase(position) member function. Let's iterate to
	// 3rd position
	it = listOfNumbers.begin();
	it++;
	it++;
	// Iterator 'it' is at 3rd position. Now erase this element.
	listOfNumbers.erase(it);
 
 
	// Iterating over list elements and display them
	it = listOfNumbers.begin();
	while(it != listOfNumbers.end())
	{
		std::cout<<(*it)<<"  ";
		it++;
	}
	std::cout<<std::endl; 
//Lets remove all elements with value greater than 3. 
listOfNumbers.remove_if([](int elem) { if(elem > 3)
					return true;
				else
					return false;
			});
 
	it = listOfNumbers.begin();
	while(it != listOfNumbers.end())
	{
		std::cout<<(*it)<<"  ";
		it++;
	}
	std::cout<<std::endl;
 
	return 0;
}
```

### \<vector\>

#### std::vector

Vectors are sequence containers representing arrays that can change in size.

``` C++
#include <vector>
int main()
{
   // This is a vector of int
    std::vector<int> vecOfInts;
 
    // While Adding it automatically adjusts it's size
    for(int i = 0; i < 10; i++)
        vecOfInts.push_back(i);
 
    std::vector<int>::iterator it = vecOfInts.begin();
    while(it != vecOfInts.end())
    {
        std::cout<<*it<<" , ";
        it++;
    }
 
    std::cout<<std::endl;
 
    for(int i = 0; i < vecOfInts.size(); i++)
        std::cout<<vecOfInts[i]<<" , ";
 
    std::cout<<std::endl;
 
    return 0;
}
```

### \<functional\>

#### std::function

An object of a function class instantiation can wrap any of the following kinds of callable objects: a function, a function pointer, a pointer to member, or any kind of function object (i.e., an object whose class defines operator(), including closures).

``` C++
#include < functional>  

std::function< size_t (const char*) > print_func;  

/// normal function -> std::function object  
size_t CPrint(const char*) { ... }  
print_func = CPrint;  
print_func("hello world"):  

/// functor -> std::function object  
class CxxPrint  
{  
public:  
    size_t operator()(const char*) { ... }  
};  
CxxPrint p;  
print_func = p;  
print_func("hello world");
```

### \<utility>

#### std::pair

Pairs: objects that can hold two values of different types: pair, make_pair, piecewise_construct, piecewise_construct_t.

``` C++
#include <iostream>
#include <utility>
#include <string>
using namespace std;
 
int main () {
pair <string,double> product1 ("tomatoes",3.25);
pair <string,double> product2;
pair <string,double> product3;
 
product2.first ="lightbulbs"; // type of first is string
product2.second =0.99; // type of second is double
 
product3 = make_pair ("shoes",20.0);
 
cout <<"The price of "<< product1.first <<" is $"<< product1.second <<"\n";
cout <<"The price of "<< product2.first <<" is $"<< product2.second <<"\n";
cout <<"The price of "<< product3.first <<" is $"<< product3.second <<"\n";
return0;
```

#### std::move

Move as rvalue. Returns an rvalue reference to arg.

```C++
{
    std::list< std::string> tokens;
    //skip initiallize...
    std::list< std::string> t1 = tokens; //copy constructor called
    std::list< std::string> t2 = std::move(tokens);  //move constructor called
}
```

#### std::forword

Returns an rvalue reference to arg if arg is not an lvalue reference.
If arg is an lvalue reference, the function returns arg without modifying its type

```C++
void processValue(int& a){ cout << "lvalue" << endl; }
void processValue(int&& a){ cout << "rvalue" << endl; }
template <typename T>
void forwardValue(T&& val)
{
    processValue(std::forward<T>(val));
}
void Testdelcl()
{
    int i = 0;
    forwardValue(i); //Call void processValue(int& a)
    forwardValue(0);//Call void processValue(int&& a)
}
```

## Key Words and Operator

### auto

Type inference.
```C++
int main()
{
    auto int foo(5); // explicitly specify that foo should have automatic duration
 
    return 0;
}
```
The auto keyword can’t be used with function parameters. `Below codes are wrong!`

```C++
#include <iostream>
 
void addAndPrint(auto x, auto y)
{
    std::cout << x + y;
}
```

### explicit

An explicit constructor can prevent unwanted implicit casting when creating an object.

``` C++
class Bar {
  public:
    /*explicit*/ Bar(int a) {  }
};

void foo(Bar b)
{
    
}

int main()
{
    foo(3); // error if constructor is explicit
    foo(Bar(3)); // works either way
}
```

### & and &&

- &: left value reference
- &&: right value reference

&& extend the life time of temp value, comepare below codes:
```C++
#include <iostream>
using namespace std;

int g_constructCount=0;
int g_copyConstructCount=0;
int g_destructCount=0;
struct A
{
    A(){
        cout<<"construct: "<<++g_constructCount<<endl;    
    }
    
    A(const A& a)
    {
        cout<<"copy construct: "<<++g_copyConstructCount <<endl;
    }
    ~A()
    {
        cout<<"destruct: "<<++g_destructCount<<endl;
    }
};

A GetA()
{
    return A();
}
```
- copy construct called by =:
```C++
int main() {
    A a = GetA();
    return 0;
}
```
Outputs:
>construct: 1
>
>copy construct: 1
>
>destruct: 1
>
>copy construct: 2
>
>destruct: 2
>
>destruct: 3

- Copy construct not called by =:
```C++
int main() {
    A&& a = GetA();
    return 0;
}
```
Outputs:
>construct: 1
>
>copy construct: 1
>
>destruct: 1
>
>destruct: 2
>

### lambda expression

The lambda expression is:
>[ captures ] (parameters) -> returnTypesDeclaration { lambdaStatements; }

[ captures ]: The capture clause, also known as the lambda introducer, specifies which outside variables are available for the lambda function and whether they should be captured by value (copying) or by reference. 

Syntax used for capturing variables :
>[]	Capture nothing (or, a scorched earth strategy?)
>
>[&]	Capture any referenced variable by reference
>
>[=]	Capture any referenced variable by making a copy
>
>[=, &foo]	Capture any referenced variable by making a copy, but capture variable foo by reference
>
>[bar]	Capture bar by making a copy; don't copy anything else
>
>[this]	Capture the this pointer of the enclosing class

```C++
#include <algorithm>
int main()
{
  int a[10] = { 9, 8, 7, 6, 5, 4, 3, 2, 1, 0 };
  std::sort( a, &a[10], [](int x, int y){ return x < y; } );
  for(int i=0; i<10; i++) { printf("%i ", a[i]); }
  printf("\n");
  return 0;
}
```

### constructor and deconstructor

Six special member functions generated by compiler:

```C++
class DataOnly {
public:
    DataOnly ()                  // default constructor
    ~DataOnly ()                 // destructor

    DataOnly (const DataOnly & rhs)         　 　  // copy constructor
    DataOnly & operator=(const DataOnly & rhs)    // copy assignment operator

    DataOnly (const DataOnly && rhs)         // C++11, move constructor
    DataOnly & operator=(DataOnly && rhs)    // C++11, move assignment operator
};
```

### delete and default

```C++
class LeafOfTree{
public:
　　LeafOfTree() = default; //default constructor
　　~LeafOfTree() = default; //default deconstructor

　　LeafOfTree(const LeafOfTree&) = delete;　　// mark copy ctor or copy assignment operator as deleted functions
　　LeafOfTree & operator=(const LeafOfTree&) = delete; 
};
```

## boost

https://www.boost.org/doc/libs/1_62_0/libs/

### optional

Class template optional is a wrapper for representing 'optional' (or 'nullable') objects who may not (yet) contain a valid value. 

```C++
boost::optional<int> convert(const std::string& text)
{
  std::stringstream s(text);
  int i;
  if ((s >> i) && s.get() == std::char_traits<char>::eof())
    return i;
  else
    return boost::none;
}
```

Observe the two return statements. return i uses the converting constructor that can create optional<T> from T. Thus constructed optional object is initialized and its value is a copy of i. The other return statement uses another converting constructor from a special tag boost::none. It is used to indicate that we want to create an uninitialized optional object.