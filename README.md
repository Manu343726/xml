# xml
The X Metaprogramming Library

## Wait, another metaprogramming library?

Currently there's an ongoing effort in the C++ community on having a general purpose metaprogramming library. Both Eric Niebler's Meta and Louis Dionne's Boost.Hana are currently pursuing for this and look very promising, but there's a little problem: **Minor, even none, support for non-cutting edge compilers**.

That's fine since projects like range-v3 and Boost.Hana are the kind of things that push compilers to their limits and make them evolve; but for day to day work having to update to the latest compiler release is not possible.  
I like both Louis's and Eric's work, I usually try to give them feedback whenever I have some time. This project is not intended as a competitor but as a way to fill the gap between pre-C++11 Boost.MPL and latest tmp efforts such as Hana and Meta. **I want a TMP library that I would be able to use at work**.

## How?

The main idea of xml is to get stuck in a C++11 only core that should work with currently stablished compilers, then write C++11/14/17 syntactic suggar layers on top of it. That is, a C++11 core that should be compatible with **VS2012, GCC 4.8.1, and Clang 3.3**.  
*That compilers were chosen from my own experience and after talking with C++ers around, but please feel free to open an issue and discuss if you are not agree*.

### Architecture

 - **core**: Core library provides a C++11 compatible set of basic features for TMP built on top of the Standard Library, such as basic high order metafunctions, type and value sequences, and support for integral and boolean algebra.
 - **utility**: Utilities component with features to ease with usual TMP-related tasks, suchas calling functions with tuples, quering for the max size type of a parameter pack, etc.
 - **suggar14**: C++14 syntactic suggar for the core features, such as Boost.Hana-like expression templates for easy manipulation of TMP constructs, variable templates for algebraic expressions, etc.

```
+-----------------------------------------+---------------------------------------------------+
|             Variable templates          |     Expression templates (overloaded operators)   |
+-----------------------------------------+---------------------------------------------------+
|  Runtime utilities (tuple_call(), etc)  |     TMP utilities (sort<>, max<>, min<>, etc)     |
+-----------------------------------------+---------------------------------------------------+ ^
|   Integral and logical algebra support  |               type/integral sequences             | |
+-----------------------------------------+---------------------------------------------------+ |
|     <type_traits> interoperability      | Metafunction-based high-order functional features | | CORE LIBRARY
|              and extensions             |          (fold, map, curry, lambda, etc)          | | 
+-----------------------------------------+---------------------------------------------------+ |
|                                      C++11 Standard Library                                 | |
+---------------------------------------------------------------------------------------------+ v
```

*Do you miss something? Please fill an issue!*

## License

All work will be licensed under the MIT license. Check LICENSE file for more info.

## Why xml?

This year I gave [a talk on tmp at Meeting C++](https://meetingcpp.com/index.php/tv15/items/4.html), talking about practical use cases of TMP and some hints about how a metaprogramming library should be designed to make it useful for the industry. I called that hypotetic library `X`, and hence the X Metaprogramming Library. Also the markup spirit of C++ tmp syntax may have affected such naming, it's angle-bracket-based compile time programming after all. [The sandwich slide](http://slides.com/manusanchez/tmpmcpp2015/live#/46) was really a delicious version of the layered diagram above.
