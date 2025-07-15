# C++

<p align="center"><img align="center" width="30%" height="30%" src="assets/cpp.svg"></p>

[C++](https://www.cplusplus.com/) is a general-purpose programming language created as an extension of the [C](https://en.wikipedia.org/wiki/C_(programming_language)) programming language.

## Index

* [Libraries](#libraries)
* [Dependencies](#dependencies)
  * [IWYU](#iwyu)
  * [PCH](#pch)
* [Null](#null)
  * [std::nullptr](#stdnullptr)
  * [std::nullptr_t](#stdnullptr_t)
* [Pointers](#pointers)
  * [std::unique_ptr](#stdunique_ptr)
  * [std::shared_ptr](#stdshared_ptr)
  * [std::weak_ptr](#stdweak_ptr)
* [Concurrency](#concurrency)
  * [std::thread](#stdthread)
  * [std::async](#stdasync)
  * [std::future](#stdfuture)
  * [std::promise](#stdpromise)
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

## Dependencies

### IWYU

[IWYU (Include What You Use)](https://include-what-you-use.org/) is a strategy (and a [tool](https://github.com/include-what-you-use/include-what-you-use)) for managing `#include` directives where core idea is `every file should include only the headers it directly uses`.

✅ Pros
* Reduces compile times (especially for large projects).
* Makes dependencies explicit and easier to track.
* Helps avoid code that breaks due to transitive includes.

❌ Cons
* Can require a lot of micro-management of includes.
* Sometimes leads to larger include lists in headers or source files.

### PCH

[PCH (Precompiled Header)](https://en.wikipedia.org/wiki/Precompiled_header) is a file (typically `pch.h`) that contains the compiled version of commonly included headers. Instead of parsing and compiling the same headers repeatedly for every source file, the compiler does it once and reuses the result.

```cpp
// pch.h
#include <iostream>
#include <map>
#include <memory>
#include <string>
#include <vector>
// ...
```

## Null

### std::nullptr

[std::nullptr](https://en.cppreference.com/w/cpp/language/nullptr.html) (C++11) is the null pointer literal.

* Type `std::nullptr_t`.
* Replaces C `NULL` macro.
* Can be implicitly converted into pointer types.
* Not convertible to integral types except `bool`.

### std::nullptr_t

[std::nullptr_t](https://en.cppreference.com/w/cpp/types/nullptr_t.html) (C++11) is the type of the null pointer literal `nullptr`.

## Pointers

### std::unique_ptr

[std::unique_ptr](https://en.cppreference.com/w/cpp/memory/unique_ptr.html) (C++11) is a smart pointer that owns and manages another object (heap-allocated memory) via a pointer and subsequently disposes of that object when the `unique_ptr` goes out of scope.

* Operators `->` and `*` are overloaded to access the object.
* The size is one pointer.

```cpp
#include <memory>

class Foo
{
public:
    void Bar(){}
};

void Process(const Foo& foo)
{
    // ...
}

void Run()
{
    std::unique_ptr<Foo> foo = std::make_unique<Foo>();

    // Call a method on the object.
    foo->Bar();

    // Pass the reference to a function.
    Process(*foo);

    // Deleted automatically when function block goes out of scope.
}

int main(int argc, char** argv)
{
    Run();
    return 0; 
}
```

### std::shared_ptr

[std::shared_ptr](https://en.cppreference.com/w/cpp/memory/shared_ptr.html) (C++11) is a smart pointer that retains shared ownership of an object through a pointer. Several `shared_ptr` objects may own the same object. The object is destroyed and its memory deallocated when the last remaining `shared_ptr` owning the object is destroyed.

* Operators `->` and `*` are overloaded to access the object.
* The size is two pointers (one for the object and one for the shared control block that contains the reference count).
* Control block access is thread-safe but manipulating the managed object is not thread-safe.

```cpp
#include <memory>

class Foo
{
public:
    void Bar(){}
};

void Process1(std::shared_ptr<Foo> foo)
{
    // ...
}

void Process2(std::shared_ptr<Foo> foo)
{
    // ...
}

int main(int argc, char** argv)
{
    std::shared_ptr<Foo> foo = std::make_shared<Foo>();

    Process1(p);
    Process2(p);

    return 0;
}
```

### std::weak_ptr

[std::weak_ptr](https://en.cppreference.com/w/cpp/memory/weak_ptr.html) (C++11) is a smart pointer that holds a non-owning (weak) reference to an object that is managed by `std::shared_ptr`. It must be converted to `std::shared_ptr` in order to access the referenced object.

* Operators `->` and `*` are overloaded to access the object.
* The size is one pointer.
* Used to observe objects that are not required to remain alive.
* Required in some cases to break circular references between `shared_ptr` instances.

## Concurrency

### std::thread

[std::thread](https://en.cppreference.com/w/cpp/thread/thread.html) (C++11) provides a standard way to write multithreaded programs accross all platforms abstracting the code from other threading APIs like POSIX `pthreads` or Windows `threads`.

```cpp
#include <iostream>
#include <thread>

void Task1()
{
    for (int i = 0; i < 100; i++)
    {
        std::cout << "(Task, 1)";
        std::cout << " (Thread ID, " << std::this_thread::get_id() << ")";
        std::cout << " (Loop, " << i << ")";
        std::cout << std::endl;
    }
}

void Task2()
{
    for (int i = 0; i < 100; i++)
    {
        std::cout << "(Task, 2)";
        std::cout << " (Thread ID, " << std::this_thread::get_id() << ")";
        std::cout << " (Loop, " << i << ")";
        std::cout << std::endl;
    }
}

int main(int argc, char** argv)
{
    std::thread worker1(Task1);
    std::thread worker2(Task2);
    
    worker1.join();
    worker2.join();
    
    return 0;
}
```

### std::async

[std::async](https://en.cppreference.com/w/cpp/thread/async.html) (C++11) provides a way to run a function asynchronously (potentially in a separate thread) and returns a `std::future` that will eventually hold the result of that function call.

Policies:
* `std::launch::async` Asynchronous execution on a new thread.
* `std::launch:deferred` Lazy evaluation on the current thread when `std::future::get` is called.

```cpp
#include <future>
#include <iostream>
#include <thread>

void Task(std::string name, int count)
{
    for (int i = 0; i < count; i++)
    {
        std::cout << "(Task, " << name << ")";
        std::cout << " (Thread ID, " << std::this_thread::get_id() << ")";
        std::cout << " (Loop, " << i << ")";
        std::cout << std::endl;
    }
}

int main(int argc, char** argv)
{
    std::future<void> future1 = std::async(std::launch::async, Task, "Task1", 100);
    std::future<void> future2 = std::async(std::launch::async, Task, "Task2", 200);

    future1.get();
    future2.get();

    return 0;
}
```

Comparing thread-based programming (`std::thread`) and task-based programming (`std::async`).

> State-of-the-art thread schedulers employ system-wide thread pools to avoid oversubscription, and they improve load balancing across hardware cores through workstealing algorithms. The C++ Standard does not require the use of thread pools or work-stealing, and, to be honest, there are some technical aspects of the C++11 concurrency specification that make it more difficult to employ them than we’d like. Nevertheless, some vendors take advantage of this technology in their Standard Library implementations, and it’s reasonable to expect that progress will continue in this area. If you take a task-based approach to your concurrent programming, you automatically reap the benefits of such technology as it becomes more widespread. If, on the other hand, you program directly with std::threads, you assume the burden of dealing with thread exhaustion, oversubscription, and load balancing yourself, not to mention how your solutions to these problems mesh with the solutions implemented in programs running in other processes on the same machine.
* Item 35, Effective Modern C++.

### std::future

[std::future](https://en.cppreference.com/w/cpp/thread/future.html) (C++11) provides a way to access the result of asynchronous operations.

* `std::future` is used by the consumer/reader of the asynchronous operation.

### std::promise

[std::promise](https://en.cppreference.com/w/cpp/thread/promise.html) (C++11) provides a way to store a value or an exception that is later acquired asynchronously via a `std::future` created by the `std::promise`.

* `std::promise` is used by the producer/writer of the asynchronous operation.

## References

* [cppreference](https://cppreference.com/)
* [Effective Modern C++](https://archive.org/details/EffectiveModernC)
* [C++ Cheat Sheets & Infographics](https://hackingcpp.com/cpp/cheat_sheets.html)
