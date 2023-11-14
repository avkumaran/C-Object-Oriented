# Derived Classes

- Derived [class](Classes) has access to public members of base class

```c++
class DerivedClass : public BaseClass { ... }
```

## Inheritance Scenarios

- Derived from base
- Derived from derived
- Derived from multiple bases

```C++
// Derived from multiple bases
class House : public Dwelling, public Property { ... }
```

## Overriding Member Functions

- Overriding — occurs with the same name and parameters
- An overriding function can call the overridden function by prepending the base class name

```c++
// Example of overriding function calling overridden function
class Restaurant : public Business {

   ...

   string GetDescription() const {
      return Business::GetDescription() + "\n  Rating: " + to_string(rating);
   };

   ...
};
```

## Protected Member Access

- "protected" access specifier provides access to derived classes

```c++
class myC {
	protected:
};
```

## Class definition Keywords

 - *public*: public-->public, protected-->protected
 - *protected*: public-->protected, protected-->protected
 - *private*: public-->private, protected-->private

```c++
class DerivedClass : protected BaseClass { ... };
```

## Polymorphism and Virtual Member Functions

- ### Polymorphism
	- **Polymorphism:** determining which behavior to execute depending on data types
		- **Compile-time polymorphism:** compiler determines which function to call at compile time
		- **Runtime polymorphism:** compiler is unable to determine which function to call at compile-time, so the determination is made while the program is running
	
		- Ex: The statement `vector<Business*> businessList;` creates a vector that can contain pointers to objects of type Business or Restaurant, since Restaurant is derived from Business.
		- Ex: `Business& primaryBusiness` declares a reference that can refer to Business or Restaurant objects.
			- **Derived/base class pointer conversion:** pointer to a derived class is converted to a pointer to the bass class without explicit casting
- ### Virtual Functions
	- *Note: Runtime polymorphism only works when an overridden member function in a base class is virtual.* 
	- **Virtual function:** member function that may be overridden in a derived class and is used for runtime polymorphism
		- Ex: `virtual string GetDescription() const`
		- *At runtime, when a virtual function is called using a pointer, the correct function to call is dynamically determined based on the actual object type to which the pointer or reference refers.*
	- The *override* keyword is optional keyword to identify an overriding function
		- Ex: `string GetDescription() const override`
- ### Pure Virtual Functions
	- **Pure virtual function:** a virtual function that provides no definition in the base class, and all derived classes must override the function
		- Ex: `virtual string GetHours() const = 0`
		- *Note: must be assigned with 0 in the base class*
	- **Abstract class:** a class that has at least one pure virtual function (an object of this class cannot be declared)

