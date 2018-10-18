# Modern C++ Review

## 1. DLL
.dll stands for dynamically link library. In contrasts to the statically link library(.lib), which is linked during the compile time, the .dll is linked dring the runtime. This means that the .dll is much more flexible since it can be updated without recompile the entire executable. 

There are two ways to export the functions from the .dll.
1. Decorate the functions with __dclspec(dllexport) keyword.
2. Use a .def file.

By using .def file, it's possible to 
1. call the functions not only by name, but also by ordinal.
2. call the functions with VB or C# 

Here is an example shows how to create and link a .dll in visual studio from Microsoft.
[Walkthrough: Create and use your own Dynamic Link Library (C++)](https://docs.microsoft.com/en-us/cpp/build/walkthrough-creating-and-using-a-dynamic-link-library-cpp?view=vs-2017)

## 2. Thread Syncronisation

## 3. Smart Pointer

## 4. Callable Targets
