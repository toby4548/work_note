# Modern C++ Review

## 1. DLL
.dll stands for dynamically link library. In contrasts to the statically link library(.lib), which is linked during the compile time, the .dll is linked dring the runtime. This means that the .dll is much more flexible since it can be updated without recompile the entire executable. 

There are two ways to export the functions from the .dll.
1. Decorate the functions with __dclspec(dllexport) keyword.
2. Use a .def file.

By using .def file, it's possible to 
1. call the functions not only by name, but also by ordinal.
2. call the functions with VB or C# 

Here is an example shows how to create and link a .dll in visual studio from Microsoft.\[Walkthrough: Create and use your own Dynamic Link Library(C++)](https://docs.microsoft.com/en-us/cpp/build/walkthrough-creating-and-using-a-dynamic-link-library-cpp?view=vs-2017)

Here is an example shows how to use .def file to export functions and call them by ordinal.\[How to use .def](https://blog.csdn.net/ithzhang/article/details/8208153)

## 2. Thread Syncronisation
Both  windows API and STL(c++11(vs2012) or later) can enable multithreading in c++ on windows.

This series introduced what is multithread programming and how to achieve it with the windows API.\[Programming Thinking - Multiprocessing and Multithreading](https://blog.csdn.net/luoweifu/article/details/46595285)

Similarily, there is another series talking about the same topic using the STL.\[C++11 Multithreading](https://thispointer.com/c-11-multithreading-part-1-three-different-ways-to-create-threads/)

## 3. Smart Pointer

## 4. Callable Targets
