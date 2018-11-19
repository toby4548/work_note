# Modern C++ Review

## 1. DLL
.dll stands for dynamically link library. In contrasts to the statically link library(.lib), which is linked during the compile time, the .dll is linked dring the runtime. This means that the .dll is much more flexible since it can be updated without recompile the entire executable. 

**DLL Main**

An optional entry point of the .dll. e.g.

```cpp
BOOL WINAPI DllMain(
  _In_ HINSTANCE hinstDLL,
  _In_ DWORD     fdwReason,
  _In_ LPVOID    lpvReserved
);
```

1. THe histDLL is a handle to the DLL module.
2. The fdwReason indicates why the entry point function is being called.
3. The lpvReseved will return the status when the process is attached/detached.

A DLL can optionally specify an entry-point function. If present, the system calls the entry-point function whenever a process or thread loads or unloads the DLL. It can be used to perform simple initialization and cleanup tasks. For example, it can set up thread local storage when a new thread is created, and clean it up when the thread is terminated.

Only one thread at a time can call the entry-point function.

**Export**

There are two ways to export the functions from the .dll.
1. Decorate the functions with __dclspec(dllexport) keyword.
2. Use a .def file.

By using .def file, it's possible to 
1. call the functions not only by name, but also by ordinal.
2. call the functions with VB or C# 

Here is an example shows how to create and link a .dll in visual studio from Microsoft.

[Walkthrough: Create and use your own Dynamic Link Library(C++)](https://docs.microsoft.com/en-us/cpp/build/walkthrough-creating-and-using-a-dynamic-link-library-cpp?view=vs-2017)

Here is an example shows how to use .def file to export functions and call them by ordinal.

[How to use .def](https://blog.csdn.net/ithzhang/article/details/8208153)

## 2. Thread Syncronisation
Both  windows API and STL(c++11(vs2012) or later) can enable multithreading in c++ on windows.

This series introduced what is multithread programming and how to achieve it with the windows API.

[Programming Thinking - Multiprocessing and Multithreading](https://blog.csdn.net/luoweifu/article/details/46595285)

Similarily, there is another series talking about the same topic using the STL.

[C++11 Multithreading](https://thispointer.com/c-11-multithreading-part-1-three-different-ways-to-create-threads/)

## 3. Smart Pointer

## 4. Callable Targets

## 5. Object Oriented Programming

### 5.1 Interface
There is no official interface in c++, but the idea can be implemented with pure virtual function.

Here is an example.

[Interface implementation in c++](https://scriptjerks.blogspot.com/2012/06/c.html)

The class IShape is an interface.

### 5.2 Patterns

There is a very comprehensive article about the implementation in c++.
[Design pattern in c++](https://segmentfault.com/a/1190000010706695)

#### Factory

The interface can be used to implement the factory design pattern

[Factory pattern](https://skyyen999.gitbooks.io/-study-design-pattern-in-java/content/factory.html)

#### Proxy

#### Singleton

## 6. Random C++ Note

**-Delete Function:（source: cppreference.com** 
If, instead of a function body, the special syntax = delete ; is used, the function is defined as deleted. Any use of a deleted function is ill-formed (the program will not compile). This includes calls, both explicit (with a function call operator) and implicit (a call to deleted overloaded operator, special member function, allocation function etc), constructing a pointer or pointer-to-member to a deleted function, and even the use of a deleted function in an unevaluated expression. However, implicit ODR-use of a non-pure virtual member function that happens to be deleted is allowed.

If the function is overloaded, overload resolution takes place first, and the program is only ill-formed if the deleted function was selected.

```cpp
struct sometype
{
    void* operator new(std::size_t) = delete;
    void* operator new[](std::size_t) = delete;
};
sometype* p = new sometype; // error: attempts to call deleted sometype::operator new
```
**Copy Slicaing**

The copy assignment from a base class to a derived class will only copy the base part from derived object.

```cpp
class Base
{
public:
  Base() { static uint32_t id = 0; mBaseId = id++; }
  virtual ~Base() = default;
  virtual std::string SomeMethod() { return std::string("BASE ").append(std::to_string(mBaseId)); }
  uint32_t mBaseId;
};

class Derived : public Base
{
public:
  Derived() { static uint32_t id = 0; mDerivedId = id++; }
  std::string SomeMethod() override { return std::string("DERIVED ").append(std::to_string(mDerivedId)); }
  uint32_t mDerivedId;
};

Derived derived;
Derived derived2;
Base& base = derived2;
base = derived;

std::cout << base.SomeMethod() << std::endl; // output: DERIVED 1
std::cout << derived2.SomeMethod() << std::endl; // output: DERIVED 1
std::cout << derived2.mBaseId << " " << derived2.mDerivedId << std::endl; // output: 0 1 CAUTION: OBJECT SCLICING!
```

Guidelines:
* Access polymorphic objects through pointers and references and don't create containers of base objects.
i.e.
```cpp

Derived derived;
std::vector<Base> vec;
vec.push_back(derived); // will create a cliced copy of derived

```
* Supress coping in base class
i.e.
```cpp
Base(const Base&)=delete;
```

**-std::vector**

1, clear() member function will call all the distructors in the container. It's a quick way to release the resource.  

## 7. Visual C++ Project Build Tricks

1. User defined macro can be saved as Project Property File. You can load them with Property Manager(VIEW -> Other Windows -> Property Manager)
2. The directories in Solution Explorer are just virtual directory.
3. For Unicode progreamming model, use **wmain** instead of **main**.
4. Change startup project: right click on project ->Set as startup project.
5. The stdafx.h is used for precompiled header.
6. To use highly accurate timestamp, check out [QPC](https://docs.microsoft.com/en-us/windows/desktop/SysInfo/acquiring-high-resolution-time-stamps)





