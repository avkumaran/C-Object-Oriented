# Function Templates

**Function template:** a function definition having a special type parameter that may be used in place of types in the function

```c++
// Example
template<typename T1, typename T2>
ReturnType FunctionName(Parameters) {
   ... 
}

// Example
template<typename T>
T TripleMin(T item1, T item2, T item3) {
   T minVal = item1; // Holds min item value, init to first item
   
   if (item2 < minVal) {
      minVal = item2;
   }
   if (item3 < minVal) {
      minVal = item3;
   }
   
   return minVal;
}
```

The type may be explicitly specified in the function call. 
	Ex: `TripleMin<int>(num1, num2, num3)`

# Class Templates

**Class template:** class definition having a special type parameter that may be used in place of types in the class
- A variable declared of that class type must indicate a specific type
	- Ex: `TripleItem<int> triShorts(99,55,66);`
- Any member functions defined outside the class declaration must be preceded by the template declaration and have the type in angle brackets appended to its name
	- Ex: `void TripleItem<T>::Print()`

```c++
// Example
template<typename T>
class TripleItem {
	public:
	   TripleItem(T val1 = 0, T val2 = 0, T val3 = 0);
	   void PrintAll() const;   // Print all data member values
	   T MinItem() const; // Return min data member value
	private:
	   T item1;           // Data value 1
	   T item2;           // Data value 2
	   T item3;           // Data value 3
};
```

```c++
// Example
template<typename T1, typename T2>
class ClassName {
	...
};
```