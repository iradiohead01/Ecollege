# C++11 Examples
- [C++11 Examples](#c11-examples)
    - [C++ STL](#c-stl)
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

## C++ STL

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