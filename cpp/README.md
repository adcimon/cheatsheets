# C++

<p align="center"><img align="center" width="30%" height="30%" src="assets/cpp.svg"></p>

[C++](https://www.cplusplus.com/) is a general-purpose programming language created as an extension of the [C](https://en.wikipedia.org/wiki/C_(programming_language)) programming language.

## Index

* [Libraries](#libraries)
* [Pointers](#pointers)
* [Concurrency](#concurrency)
  * [std::thread](#stdthread)
  * [std::async](#stdasync)
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
    std::future<void> future1 = std::async(std::launch::async, Task1);
    std::future<void> future2 = std::async(std::launch::async, Task2);

    future1.get();
    future2.get();

    return 0;
}
```

Comparing thread-based programming (`std::thread`) and task-based programming (`std::async`).

> State-of-the-art thread schedulers employ system-wide thread pools to avoid oversubscription, and they improve load balancing across hardware cores through workstealing algorithms. The C++ Standard does not require the use of thread pools or work-stealing, and, to be honest, there are some technical aspects of the C++11 concurrency specification that make it more difficult to employ them than we’d like. Nevertheless, some vendors take advantage of this technology in their Standard Library implementations, and it’s reasonable to expect that progress will continue in this area. If you take a task-based approach to your concurrent programming, you automatically reap the benefits of such technology as it becomes more widespread. If, on the other hand, you program directly with std::threads, you assume the burden of dealing with thread exhaustion, oversubscription, and load balancing yourself, not to mention how your solutions to these problems mesh with the solutions implemented in programs running in other processes on the same machine.
* Item 35, Effective Modern C++.

## References

* [cppreference](https://cppreference.com/)
* [Effective Modern C++](https://archive.org/details/EffectiveModernC)
* [C++ Cheat Sheets & Infographics](https://hackingcpp.com/cpp/cheat_sheets.html)
* [Smart Pointers](https://docs.microsoft.com/en-us/cpp/cpp/smart-pointers-modern-cpp)
