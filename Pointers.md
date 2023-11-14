**Pointer:** holds memory address
	Declaration ex: `int* myIntPointer;`

The **reference operator** (`&`) obtains a variable's address: `&varName`

The **dereference operator** (`*`) is used to retrieve what the pointer is pointing to
	Ex: `*myIntPointer`

A pointer can be assigned with `nullptr` or `NULL`. Both mean the same thing

## Operators

***new* operator**: allocates memory for the given type and returns a pointer to the allocated memory. If the type is a class, the new operator calls the class's constructor after allocating memory for the class's member variables.
	Ex: `MyClass* myObject = new MyClass;`
	Ex: `MyClass* myObject = new MyClass(ctorArg1, ctorArg2);`

	- The new operator creates a dynamically allocated array of objects if the class name is followed by square brackets containig the array's length. A single, contiguous chunk of memory is allocated for the array, then the default constructor is called for each object in the array. A compiler error occurs if the class does not have a constructor that can take 0 arguments.

**Member access operator:** `->`, which is the equivalent of `(*a).b`
	Ex: `a->b`

***Delete* operator:** deallocates a block of memory that was allocated with the *new* operator
	Ex: `delete pointerVariable;`

***delete[]* operator**: used to free an array allocated with the new operator







