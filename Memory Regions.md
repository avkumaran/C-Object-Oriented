-   **Code** — The region where the program instructions are stored.

-   **Static memory** — The region where global variables (variables declared outside any function) as well as static local variables (variables declared inside functions starting with the keyword "static") are allocated. Static variables are allocated once and stay in the same memory location for the duration of a program's execution.

-   **The stack** — The region where a function's local variables are allocated during a function call. A function call adds local variables to the stack, and a return removes them, like adding and removing dishes from a pile; hence the term "stack." Because this memory is automatically allocated and deallocated, it is also called automatic memory.

-   **The heap** — The region where the "new" operator allocates memory, and where the "delete" operator deallocates memory. The region is also called free store.