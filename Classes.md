# Basics 
**Class:** type that can group data and functions to form an object

***Public* designator:** can be accessed by class users using member access operator `.`
***Private* designator:** can only be accessed by member functions of the class

Function definitions outside of class definition must use scope resolution operator.

```c++
class MyClass {
  public:
     void Fct1(); 

  private:
     int numA;
};

void MyClass::Fct1() {
  numA = 0;
}
```

**Inline member function:** a function defined within the class definition

Programmers typically put all code for a class into two files, separate from other code.
-   **ClassName.h** contains the class definition, including data members and member function declarations
-   **ClassName.cpp** contains member function definitions

A file that uses the class, such as a main file or ClassName.cpp, must include ClassName.h.

Member functions
1) Mutators (setters)
2) Accessors (getters)
	- Use *const* keyword. Ex: `string GetName() const;`

# Constructors

Default constructor having no statements is provided by compiler *if no constructor is explicitly defined*

Constructors have no return type.

A constructor's parameters by be assigned default values. If those default values allow th econstructor to be called without arguments, then it can serve as the default constructor. (*Note: default values can be provided in the function declaration or in the definition but not both*)

## Initializer Lists

```c++
// Non-initializer list method
SampleClass::SampleClass() {
   field1 = 100;
   field2 = 200;
}

// Initializer list method
SampleClass::SampleClass() : field1(100), field2(200) {
}
```

Initializer lists are important when a data member is a class type that must be explicitly constructed instead of default constructed.

```c++
SampleClass::SampleClass() {
   // itemList gets default constructed, size 0  
   itemList.resize(2);
}

SampleClass::SampleClass() : itemList(2) {
   // itemList gets constructed with size 2
}
```

## Copy Constructors

If not explicitly defined, the compiler provides a copy constructor that performs a memberwise copy (shallow copy).

Explicitly writing a copy constructor is necessary for classes that have pointer data members.

```c++
// MyClass has data member: int* dataObject;

MyClass::MyClass(const MyClass& origObject) {
   dataObject = new int; // Allocate sub-object
   *dataObject = *(origObject.dataObject);
}
```

Ex of use of copy constructor: `MyClass classObj2 = classObj1;` or `obj2Ptr = new MyClass(classObj1);`

# Copy Assignment Operator

Default behavior of assignment operator(`=`) is shallow copy

If you want a deep copy, explicitly define the copy assignment operator

```c++
MyClass& MyClass::operator=(const MyClass& objToCopy) {

   if (this != &objToCopy) {      // 1. Don't self-assign
      delete dataObject;          // 2. Delete old dataObject
      dataObject = new int;       // 3. Allocate new dataObject
      *dataObject = *(objToCopy.dataObject); // 4. Copy dataObject
   }
   
   return *this;
}
```

# Destructors

A destructor has no parameters and no return value

```c++
// Destructor for LinkedList class
LinkedList::~LinkedList() {
   // The destructor deletes each node in the linked list
   while (head) {
      LinkedListNode* next = head->next;
      delete head;
      head = next;
   }
}
```

**When is a destructor is called?** When using the delete operator on an object allocated with the new operator. For an object not declared by reference or by pointer, the object's destructor is called automatically when the object goes out of scope.

# The Implicit Parameter

The object calling a member function is passed into the function implicitly as a pointer called *this*.

```c++
void ShapeSquare::SetSideLength(double sideLength) {
   this->sideLength = sideLength;   // Data member      Parameter
}
/* Note the "this" in this example is mandatory since the function parameter is also called sideLength */
```

# Operator Overloading

```c++
class TimeHrMn {
	public:
	   TimeHrMn(int timeHours = 0, int timeMinutes = 0);
	   void Print() const;
	   TimeHrMn operator+(TimeHrMn rhs) ;
	private:
	   int hours;
	   int minutes;
};

// Overload + operator for TimeHrMn
TimeHrMn TimeHrMn::operator+(TimeHrMn rhs) {
   TimeHrMn timeTotal;
   
   timeTotal.hours   = hours   + rhs.hours;
   timeTotal.minutes = minutes + rhs.minutes;
   
   return timeTotal;
}
```

With an overloaded + operator, something like `time1 + time2` becomes valid.
`time1.operator+(time2)` is technically also valid but almost never used.

An operator can be overloaded multiple times for different types

Be sure to use const when necessary

## Comparison Operators

These are not made as member functions, but rather have two parameters that can be class objects
	Ex: `bool operator==(const MyClass& lhs, const MyClass& rhs)`

Ex:
```c++
// Less-than (<) operator for two Review objects
bool operator<(const Review& lhs, const Review& rhs) {
   return lhs.GetRating() < rhs.GetRating();
}
```


