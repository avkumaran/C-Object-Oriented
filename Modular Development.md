**Modular compilation** approach can be used that separates the compiling and linking steps within the compilation process. 
- Each source file is independently compiled into an object file. An object file contains machine instructions for the compiled code along with placeholders, often referred to as references, for calls to functions or accesses to variables or classes defined in other source files or libraries.
	- Ex: `g++ -c main.cpp`

- After each source file has been compiled, the linker will create the final executable by linking together the object files and libraries. For each placeholder found within an object file, the linker searches the other object files and libraries to find the referenced function or variable. Once all placeholders have been linked together, the final executable can be created.
	- Ex: `g++ -o exeName main.o class1.o class2.o`

Running the program on Mac: `./exeName`
