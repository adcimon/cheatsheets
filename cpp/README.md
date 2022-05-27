# C++

<p align="center"><img align="center" width="30%" height="30%" src="assets/cpp.svg"></p>

[C++](https://www.cplusplus.com/) is a general-purpose programming language created as an extension of the [C](https://en.wikipedia.org/wiki/C_(programming_language)) programming language.

## Index

* [Libraries](#libraries)
* [Pointers](#pointers)
* [References](#references)

## Libraries

A [library](https://en.wikipedia.org/wiki/Library_(computing)) is a collection of resources used by programs. These resources may include code, data, templates, documentation, etc.

There are 2 types of libraries, [static](https://en.wikipedia.org/wiki/Static_library) and [dynamic](https://en.wikipedia.org/wiki/Dynamic-link_library).

* Static files (`lib`) can contain either `static` libraries (containing object files) or `import` libraries (containing symbols to allow the linker to link `dll` or `so` files).
* Dynamic files (`dll` or `so`) contain `dynamic` libraries.

When linking is performed during the creation of an executable or an object file, it is known as [static linking](https://en.wikipedia.org/wiki/Library_(computing)#Static_libraries) ([early binding](https://en.wikipedia.org/wiki/Name_binding)). In this case, the linking is usually done by a linker, but may also be done by the compiler.

When linking is performed while a program is being loaded ([load time](https://en.wikipedia.org/wiki/Loader_(computing))) or executed ([runtime](https://en.wikipedia.org/wiki/Runtime_(program_lifecycle_phase))), it is known as [dynamic linking](https://en.wikipedia.org/wiki/Dynamic_linker) ([late binding](https://en.wikipedia.org/wiki/Late_binding)).

Dynamic libraries have 2 types of linking.
* Implicit. When a `lib` file is provided by the `dll` creator along with appropriate headers. This `lib` is an `import` library, merely a descriptor of the target library, it contains entry point, addresses, etc. It doesn't contain any code and must be passed to the linker.
* Explicit. When the library is manually loaded with `LoadLibrary` functions. The `lib` file isn't needed, but it requires more effort to find exports, addresses, and call functions through pointers.

## Pointers

* `raw pointer`<br>

* `unique_ptr`<br>
Allows exactly one owner of the underlying pointer. Use as the default choice for POCO unless you know for certain that you require a `shared_ptr`. Can be moved to a new owner, but not copied or shared.
```
void MyFunction()
{    
    // Create the object and pass it to a unique pointer.
    std::unique_ptr<MyClass> p(new MyClass());

    // Call a method on the object.
    p->DoSomething();

    // Pass a reference to a method.
    ProcessObject(*p);
}
// Unique pointer is deleted automatically when function block goes out of scope.
```

* `shared_ptr`<br>
Reference-counted smart pointer. Use when you want to assign one raw pointer to multiple owners, for example, when you return a copy of a pointer from a container but want to keep the original. The raw pointer is not deleted until all `shared_ptr` owners have gone out of scope or have otherwise given up ownership. The size is two pointers, one for the object and one for the shared control block that contains the reference count.

* `weak_ptr`<br>
Special-case smart pointer for use in conjunction with `shared_ptr`. A `weak_ptr` provides access to an object that is owned by one or more `shared_ptr` instances, but does not participate in reference counting. Use when you want to observe an object, but do not require it to remain alive. Required in some cases to break circular references between `shared_ptr` instances.

## References

* [C++ Cheat Sheets & Infographics](https://hackingcpp.com/cpp/cheat_sheets.html)
* [Smart Pointers](https://docs.microsoft.com/en-us/cpp/cpp/smart-pointers-modern-cpp)
