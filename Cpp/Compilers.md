# Compilers

## Stages of Compilation in C++

### Preprocessing

The first stage is the preprocessing of the source code.
Preprocessors modify the source code before the actual compilation process.
They handle directives that start with a `#` (hash) symbol, like `#include`, `#define`, and `#if`.
In this stage, included header files are expanded, macros are replaced, and conditional compilation statements are processed.

### Compilation

The second stage is the actual compilation of the preprocessed source code.
The compiler translates the modified source code into an intermediate representation, usually specific to the target processor architecture.
This step also involves performing syntax checking, semantic analysis, and producing error messages for any issues encountered in the source code.

### Assembly

The third stage is converting the compiler’s intermediate representation into assembly language.
This stage generates assembly code using mnemonics and syntax that is specific to the target processor architecture.
Assemblers then convert this assembly code into object code (machine code).

### Linking

The final stage is the linking of the object code with the necessary libraries and other object files.
In this stage, the linker merges multiple object files and libraries, resolves external references from other modules or libraries, allocates memory addresses for functions and variables, and generates an executable file that can be run on the target platform.
