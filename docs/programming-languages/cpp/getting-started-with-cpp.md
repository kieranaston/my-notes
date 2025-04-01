# Getting started with C++

## Idiosyncracies

Every C++ program needs to have a main function. The operating system calls `main` to run your C++ program.

###Function definitions - four components
1. Return type
2. Function name
3. Parameter list
4. Function body

`main` must have a return type of `int` since it is used to indicate the success/failure of a program. Different `int` values used to indicate successes/failutres of different types.

Semicolons are required at the end of each line.

Different compilers use different file-naming conventions.

###Compiling and running files
1. `clang++ filename.cpp -o filename`
2. `./filename`

Extensions for executables vary from Windows to UNIX operating systems.

The `-Wall` specifier can be used to generate warnings with the GNU compiler, while `/W4` can be used with Microsoft compilers.

###Input and output

Input and output utilities are included wit the standard library but not part of the language itself.

A "stream" is an important concept in the context of C++, and refers to a sequence of characters read from or written to an IO device.

The standard output object (as part of the standard library) is `cout`, while the standard input object is `cin`. The standard library also defines `cerr` and `clog` for standard error and general info about the execution of the program, respectively.

