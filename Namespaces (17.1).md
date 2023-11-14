**Namespace:** a scope within which things are defined. Helps prevent name conflicts
	A scope resolution operator `::` must be used to access things within a scope
```c++
// auditorium.h
namespace auditorium {
   class Seat { 
      ... 
   };
}
```

```c++
#include "auditorium.h"

int main() {
   auditorium::Seat concertSeat; 

   // ...

   return 0;
}
```

Using a namespace:
1.  **_Scope resolution operator (::):_** A programmer can use the scope resolution operator to specify the std namespace. Ex: `std::cout << "Hello";` or `std::string userName;`
2.  **Namespace directive**: A programmer can add the statement  `using namespace nameOfNamespace;` to direct the compiler to check the namespace for any names later in the file that aren't otherwise declared

