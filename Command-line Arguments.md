```c++
int main(int argc, char* argv[]) {
   int i;

   // Prints argc and argv values
   cout << "argc: " << argc << endl;
   for (i = 0; i < argc; ++i) {
      cout << "argv[" << i << "]: " << argv[i] << endl;
   }

   return 0;
}
```

The system passes an int parameter argc to main() indicating the number of command-line arguments. The number includes the program name itself.

The system passes a second parameter argv to main() defined as an array of strings. `argv[0]` is the program name.

Make sure to check how many arguments were entered by the user to avoid out-of-range array access.

`atoi()` converts a C string to an integer, and is made available via `#include <cstdlib>`.

For the program user: putting quotes around an argument allows an argument's string to have any number of spaces