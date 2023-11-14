# Exception-Handling Constructs

***try*** **block**: surrounds normal code. Exited immediately if throw executes
***throw*** **statement**: appears within a try block
	- provides an object of a particular type
***catch*** **clause** (handler): immediately follows a try block
	- clause executes if the catch clause parameter type matches the exception type thrown
	- ***catch(...)***: catch-all handler that catches any type

```c++
// Basic Syntax
...
try {
	...
	// If error detected
		// throw objectOfExceptionType;
	...
}
catch (exceptionType excptObj) {
	// Handle exception
}
```

```c++
#include <iostream>
#include <stdexcept>
using namespace std;

int main() {
   int weightVal;       // User defined weight (lbs)
   int heightVal;       // User defined height (in)
   float bmiCalc;       // Resulting BMI
   char quitCmd;        // Indicates quit/continue

   quitCmd = 'a';
   
   while (quitCmd != 'q') {
      
      try {         // Get user data
         cout << "Enter weight (in pounds): ";
         cin >> weightVal;
         
         // Error checking, non-negative weight
         if (weightVal < 0) {
            throw runtime_error("Invalid weight.");         }
         
         cout << "Enter height (in inches): ";
         cin >> heightVal;
         
         // Error checking, non-negative height
         if (heightVal < 0) {
            throw runtime_error("Invalid height.");         }
         
         // Calculate BMI and print user health info if no input error
         // Source: http://www.cdc.gov/
         bmiCalc = (static_cast<float>(weightVal) /
                    static_cast<float>(heightVal * heightVal)) * 703.0;
         
         cout << "BMI: " << bmiCalc << endl;
         cout << "(CDC: 18.6-24.9 normal)" << endl;
      }
      catch (runtime_error& excpt) {         // Prints the error message passed by throw statement
         cout << excpt.what() << endl;
         cout << "Cannot compute health info." << endl;
      }
      
      // Prompt user to continue/quit
      cout << endl << "Enter any key ('q' to quit): ";
      cin >> quitCmd;
   }
   
   return 0;
}
```


Types within `#include <stdexcept>`
| Type | Reason Exception is Thrown |
| --- | ---|
| bad_alloc | Failure in allocating memory
| ios_base::failure | Failure in a stream (Ex: cin, stringstream, fstream)
| logic_error | To report errors in a program's logic Ex: out_of_range error (index out of bounds) |
| runtime_error | To report errors that can only be detected at runtime. Ex: overflow_error (arithmetic overflow) |

If an exception is thrown within a function and not caught within that function, then the function is immediately exited and the calling function is checked for a handler, and so on up the function call hierarchy. If no handler is found going up the call hierarchy, then terminate() is called, which typically aborts the program.

A catch block with type base class will handle exceptions of type derived class. So be careful with the ordering of catch blocks.