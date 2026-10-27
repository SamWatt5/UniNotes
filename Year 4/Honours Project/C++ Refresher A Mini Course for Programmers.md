# C++ Refresher: A Mini Course for Programmers

Sep 30, 2026 · @Sam Watts

## How to use this course

Seven short modules plus a capstone, aimed at roughly 10–15 hours total. Each module is a quick syntax tour, the C++-specific traps, and one small exercise. It assumes you already know variables, loops, OOP and data structures, and targets **C++20**.

**Setup (Linux/macOS/WSL):**

```bash
sudo apt install g++ cmake gdb        # or clang++; macOS: xcode-select --install && brew install cmake
g++ --version                         # want 11+ for solid C++20 support
```

For quick single-file exercises, compile with warnings and sanitizers on. They catch most memory bugs the moment they happen, which is the single biggest help when relearning:

```bash
g++ -std=c++20 -Wall -Wextra -Wpedantic -g -fsanitize=address,undefined main.cpp -o main && ./main
```

Editor: VS Code with the clangd extension (or CLion, free for students) gives you proper autocompletion and inline errors. Keep [cppreference.com](https://en.cppreference.com) open; it is the reference everyone uses.

**Suggested repo layout** (you will build towards this in Module 2 and use it for the capstone):

```
cpp-refresher/
├── CMakeLists.txt
├── include/        # .hpp headers
├── src/            # .cpp implementation + main.cpp
└── exercises/      # one file per module exercise
```

## Module 1: Syntax refresher

C++ looks like Java but behaves closer to C: values are copied by default, nothing is garbage collected, and the compiler assumes you know what you are doing.

```cpp
#include <iostream>   // std::cout, std::cin
#include <string>
#include <vector>

int square(int x) { return x * x; }          // declare-before-use: define above main or declare a prototype

int main() {
    int n = 5;                  // fixed-size ints: int, long, long long; also <cstdint>: int32_t, uint64_t
    double d{3.14};             // brace init: refuses narrowing conversions (int i{3.7} won't compile)
    auto s = std::string{"hi"}; // auto deduces the type
    const int max = 10;         // immutable
    constexpr int k = 4 * 4;    // computed at compile time

    std::vector<int> v = {1, 2, 3};
    for (int x : v) std::cout << x << ' ';          // range-for (copies each element)
    for (const auto& x : v) std::cout << x << ' ';  // range-for by const reference (no copy) — use this by default
    for (std::size_t i = 0; i < v.size(); ++i) {}  // classic loop; size() is unsigned

    std::string name;
    std::cin >> name;                       // reads one word
    std::cout << "Hello, " << name << "\n"; // prefer "\n" over std::endl (endl also flushes)

    if (auto len = name.size(); len > 3) {} // if with initialiser (C++17)
    return 0;                               // main returns int; 0 = success
}
```

**C++-isms to relearn here:**

- **Uninitialised variables hold garbage.** `int x;` inside a function is not zero. Always initialise.
- **`std::` everywhere.** Avoid `using namespace std;`, especially in headers; it causes name clashes.
- **Integer division and overflow.** `7 / 2 == 3`, and signed overflow is undefined behaviour, not wraparound.
- **Mixing signed and unsigned** (`int i < v.size()`) triggers warnings for good reason: `-1 < v.size()` can be false.
- **`std::string` is a value.** Assigning copies it; comparing with `==` compares contents (unlike Java).
- **Structs** are just classes with public-by-default members: `struct Point { double x{}, y{}; };`
- **Enums:** prefer `enum class Colour { Red, Green };`, which is scoped and doesn't implicitly convert to int.

**Exercise 1:** Write a program that reads integers from `std::cin` until EOF (`while (std::cin >> x)`), stores them in a `std::vector<int>`, and prints the count, sum, min, max and mean. Compile with the sanitizer command from setup.

## Module 2: Header files and the build

Each `.cpp` file is compiled on its own into an object file, then the linker stitches them together. Headers exist so every `.cpp` can see the *declarations* it needs, while each *definition* lives in exactly one `.cpp`.

1. **Preprocess:** `#include` literally pastes the header's text in.
2. **Compile:** each `.cpp` (a "translation unit") becomes a `.o` file. Errors here are syntax/type errors.
3. **Link:** the `.o` files are combined. "undefined reference to…" means a declaration had no definition; "multiple definition of…" means something was defined in two places (usually a function body in a header).

```cpp
// include/stack.hpp — declarations
#pragma once                 // include guard: stops the header being pasted twice
#include <vector>

class IntStack {
public:
    void push(int value);
    int pop();
    bool empty() const;
private:
    std::vector<int> data_;
};

int clamp(int v, int lo, int hi);   // free function declaration
```

```cpp
// src/stack.cpp — definitions
#include "stack.hpp"         // quotes = your headers, <angle brackets> = system/library headers
#include <stdexcept>

void IntStack::push(int value) { data_.push_back(value); }   // ClassName:: says which class this belongs to

int IntStack::pop() {
    if (data_.empty()) throw std::out_of_range("pop on empty stack");
    int top = data_.back();
    data_.pop_back();
    return top;
}

bool IntStack::empty() const { return data_.empty(); }

int clamp(int v, int lo, int hi) { return v < lo ? lo : (v > hi ? hi : v); }
```

**Rules of thumb:**

- Headers hold declarations, class definitions, templates, and `inline`/`constexpr` functions. Everything else goes in `.cpp`.
- Include what you use; don't rely on another header happening to include it for you.
- Forward-declare (`class Foo;`) in a header when you only need a pointer or reference to `Foo`, to cut compile times and break include cycles.
- `#pragma once` is universally supported; the older equivalent is `#ifndef STACK_HPP / #define STACK_HPP / #endif`.

**CMake** (you'll almost certainly want this for the honours project):

```cmake
cmake_minimum_required(VERSION 3.20)
project(cpp_refresher CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)   # lets clangd understand your project

add_executable(app src/main.cpp src/stack.cpp)
target_include_directories(app PRIVATE include)
target_compile_options(app PRIVATE -Wall -Wextra -Wpedantic)
```

```bash
cmake -S . -B build -DCMAKE_BUILD_TYPE=Debug
cmake --build build && ./build/app
```

**Exercise 2:** Split the `IntStack` above into the repo layout from setup, write a `main.cpp` that uses it, and build with CMake. Then deliberately break it three ways and read the errors: remove the `#include "stack.hpp"` from `main.cpp`, remove `src/stack.cpp` from `add_executable`, and move a function body into the header without `inline` and include it from two files.

## Module 3: Pointers, references and memory

A pointer is a variable holding an address that can be null and reseated; a reference is an alias that must bind at creation and can never change. Default to references for parameters, and use pointers when "nothing" is a valid value.

```cpp
int a = 10;
int* p = &a;      // & in an expression = "address of"; * in a type = "pointer to"
*p = 20;          // * in an expression = dereference; a is now 20
int& r = a;       // & in a type = reference; r IS a
r = 30;           // a is now 30

int* q = nullptr; // never use NULL or 0 in modern C++
if (q) { /* safe to use *q */ }

struct Point { double x, y; };
Point pt{1, 2};
Point* pp = &pt;
pp->x = 5;        // -> is (*pp).x
```

**Passing arguments** — the choice you'll make most often:

| Signature | Meaning | Use when |
| --- | --- | --- |
| `void f(int x)` | copy | small types (int, double, pointers) |
| `void f(const std::string& s)` | read-only, no copy | large types you only read |
| `void f(std::string& s)` | caller's object, modifiable | output / in-out parameters |
| `void f(std::string* s)` | may be null, modifiable | optional parameter |
| `void f(std::string s)` | own copy (can be moved in) | you'll store or modify it anyway |

**`const` placement** (read right to left):

```cpp
const int* p1;        // pointer to const int: can't change *p1, can reseat p1
int* const p2 = &a;   // const pointer to int: can change *p2, can't reseat p2
const int* const p3 = &a;  // neither
```

**Stack vs heap:** local variables live on the stack and die at the end of their scope. `new` puts things on the heap, and they live until you `delete` them. In modern C++ you almost never write `new`/`delete` yourself (Module 4 shows why), but you need to recognise them:

```cpp
int* h = new int(5);      delete h;
int* arr = new int[10];   delete[] arr;   // array form must match
```

**Arrays:** a raw array `int nums[5]` decays to a pointer when passed to a function and loses its size. Prefer `std::array<int, 5>` (fixed) or `std::vector<int>` (dynamic). Pointer arithmetic (`*(p + 2)`) works but is mostly for low-level code.

**The classic bugs** (the sanitizer catches all of these):

- **Dangling pointer/reference:** returning `&local` or a reference to a local from a function. The local is gone once the function returns.
- **Use after free:** using a pointer after `delete`.
- **Double free** and **memory leaks:** deleting twice, or never.
- **Iterator/pointer invalidation:** holding a pointer into a `std::vector`, then `push_back` reallocates and it now dangles.

**Exercise 3:** Write `void swap_ints(int* a, int* b)` and `void swap_ints(int& a, int& b)` (overloading is fine), and a function `const Point* find_closest(const std::vector<Point>& pts, Point target)` that returns `nullptr` for an empty vector. Then write a function that returns a reference to a local, compile it, and read the warning and the sanitizer report.

## Module 4: RAII and smart pointers

RAII ("Resource Acquisition Is Initialisation") is the most important idea in C++: tie every resource to an object's lifetime, acquire it in the constructor, release it in the destructor. Destructors run automatically when an object goes out of scope, even when an exception is thrown, so cleanup can't be forgotten. It's C++'s answer to Python's `with` and Java's try-with-resources, except it applies to everything.

```cpp
#include <fstream>
#include <mutex>

void write_log(const std::string& msg) {
    std::ofstream file("log.txt", std::ios::app);   // opens here
    file << msg << "\n";
}                                                   // closes here, automatically

std::mutex m;
void safe_increment(int& counter) {
    std::lock_guard<std::mutex> lock(m);  // locks
    ++counter;
}                                         // unlocks, even if an exception flew
```

**Smart pointers** (`#include <memory>`) apply RAII to heap memory, which is why you rarely write `new`/`delete`:

| Type | Ownership | Create with | Notes |
| --- | --- | --- | --- |
| `std::unique_ptr<T>` | one owner | `std::make_unique<T>(args...)` | default choice; zero overhead; move-only |
| `std::shared_ptr<T>` | shared, ref-counted | `std::make_shared<T>(args...)` | freed when the last owner goes; some overhead |
| `std::weak_ptr<T>` | non-owning observer of a `shared_ptr` | from a `shared_ptr` | breaks reference cycles; `.lock()` to use |
| `T*` / `T&` (raw) | non-owning | `.get()` / `*ptr` | fine for "I'm just looking at it" |

```cpp
#include <memory>
#include <vector>

struct Shape { virtual ~Shape() = default; virtual double area() const = 0; };
struct Circle : Shape { double r; explicit Circle(double r) : r(r) {} double area() const override { return 3.14159 * r * r; } };

int main() {
    auto c = std::make_unique<Circle>(2.0);
    // auto c2 = c;             // compile error: unique_ptr can't be copied
    auto c2 = std::move(c);     // ownership transferred; c is now null

    std::vector<std::unique_ptr<Shape>> shapes;   // polymorphic container: the standard pattern
    shapes.push_back(std::make_unique<Circle>(1.0));
    for (const auto& s : shapes) std::cout << s->area() << "\n";
}   // everything freed here, no delete anywhere
```

**Rules:**

- A function *taking* `std::unique_ptr<T>` by value means "I take ownership". If it only uses the object, take `T&` or `const T&` (or `T*` if nullable).
- Reach for `shared_ptr` only when ownership is genuinely shared; it is often a sign of an unclear design.
- Base classes used polymorphically need a `virtual` destructor, or deleting through a base pointer skips the derived destructor.

**Exercise 4:** Write a `Timer` class whose constructor records `std::chrono::steady_clock::now()` and whose destructor prints the elapsed milliseconds. Use it as `{ Timer t; expensive_work(); }`. Then convert any `new`/`delete` from Exercise 3 to `std::unique_ptr`.

## Module 5: Classes, copying and moving

C++ classes are value types: `Foo b = a;` makes a full copy, and the compiler writes copy/move operations for you unless you stop it. Most of the time you want it to (the Rule of Zero); you only step in when a class directly owns a raw resource.

```cpp
class Account {
public:
    Account(std::string owner, double balance = 0.0)         // default argument
        : owner_(std::move(owner)), balance_(balance) {}     // member initialiser list: use it, not assignment in the body

    explicit Account(double balance) : Account("anon", balance) {}  // delegating ctor; explicit blocks `Account a = 5.0;`

    const std::string& owner() const { return owner_; }     // const method: promises not to modify *this
    double balance() const { return balance_; }
    void deposit(double amt);                                // defined in the .cpp

    bool operator==(const Account&) const = default;         // C++20: compiler-written comparison
    friend std::ostream& operator<<(std::ostream& os, const Account& a) {
        return os << a.owner_ << ": " << a.balance_;
    }

private:
    std::string owner_;
    double balance_{0.0};   // default member initialiser
};
```

**Things that differ from Java/Python:**

- Members are initialised in **declaration order**, not initialiser-list order. Keep them the same to avoid bugs.
- A `const` object (or a `const&` parameter) can only call `const` methods. Mark every method that doesn't modify state as `const`, or you'll hit errors later.
- `static` members belong to the class; `virtual` must be explicit, and `override` should always be written on overrides so the compiler checks you.
- Objects stored by value in a `std::vector<Base>` get **sliced** (derived parts cut off). Store `std::unique_ptr<Base>` for polymorphism.

**Rule of 0 / 3 / 5.** The five special members are the destructor, copy constructor, copy assignment, move constructor and move assignment.

- **Rule of 0 (aim for this):** use members like `std::string`, `std::vector`, `std::unique_ptr` that already manage themselves, and declare none of the five.
- **Rule of 5:** if you must write one (e.g. a destructor that frees a raw handle), write or `= delete` all five.

```cpp
class Buffer {                              // owns a raw array, so it needs all five
public:
    explicit Buffer(std::size_t n) : size_(n), data_(new int[n]{}) {}
    ~Buffer() { delete[] data_; }

    Buffer(const Buffer& o) : size_(o.size_), data_(new int[o.size_]) {       // copy: deep copy
        std::copy(o.data_, o.data_ + size_, data_);
    }
    Buffer& operator=(Buffer o) noexcept { swap(o); return *this; }            // copy-and-swap handles copy AND move assignment

    Buffer(Buffer&& o) noexcept : size_(o.size_), data_(o.data_) {            // move: steal the pointer
        o.size_ = 0; o.data_ = nullptr;
    }
    void swap(Buffer& o) noexcept { std::swap(size_, o.size_); std::swap(data_, o.data_); }

private:
    std::size_t size_;
    int* data_;
};
```

**Move semantics in one paragraph:** `T&&` is an rvalue reference, binding to temporaries or to things you've marked with `std::move`. `std::move(x)` doesn't move anything; it's a cast that says "I'm done with `x`, you may steal its guts". After a move, `x` is valid but unspecified, so only assign to it or destroy it. Mark move operations `noexcept`, or `std::vector` will copy instead of move when it grows.

**Exercise 5:** Implement the `Buffer` class above in its own header/source, add `operator[]` (const and non-const versions) and `size()`. Put print statements in each special member, then write tests that trigger each one: `Buffer b = a;`, `b = a;`, `Buffer c = std::move(a);`, and returning a `Buffer` from a function (notice copy elision often skips the move entirely). Finally, replace `int*` with `std::vector<int>` and delete all five, which is the Rule of Zero in action.

## Module 6: The standard library (STL)

The STL is containers + iterators + algorithms: algorithms work on iterator ranges, so any algorithm works with any container. `std::vector` should be your default container; reach for others only with a reason.

| Container | Like (Python/Java) | Use when |
| --- | --- | --- |
| `std::vector<T>` | list / ArrayList | default; contiguous, fast iteration |
| `std::array<T, N>` | fixed array | size known at compile time |
| `std::string` | str / String | text (mutable, unlike Python/Java) |
| `std::unordered_map<K, V>` | dict / HashMap | key lookup, order irrelevant |
| `std::map<K, V>` | TreeMap | keys kept sorted |
| `std::unordered_set<T>` / `std::set<T>` | set / HashSet / TreeSet | membership tests |
| `std::deque<T>`, `std::queue`, `std::stack`, `std::priority_queue` | deque / Queue / Stack / PriorityQueue | the obvious use cases |
| `std::optional<T>` | Optional / None | a value that might be absent |
| `std::pair`, `std::tuple` | tuple | small bundles; unpack with `auto [a, b] = p;` |

```cpp
#include <algorithm>
#include <numeric>
#include <unordered_map>
#include <ranges>

std::vector<int> v = {5, 3, 8, 1};
v.push_back(9);            // append
v.emplace_back(4);         // construct in place (useful for objects)

std::sort(v.begin(), v.end());                                  // classic iterator-pair style
std::ranges::sort(v, std::greater{});                           // C++20 ranges: pass the container
auto it = std::ranges::find(v, 8);
if (it != v.end()) std::cout << "found at " << (it - v.begin()); // end() = "one past the last" = not found
int total = std::accumulate(v.begin(), v.end(), 0);

// lambdas: [capture](params) { body }
int threshold = 4;
auto big = std::ranges::count_if(v, [threshold](int x) { return x > threshold; });
std::erase_if(v, [](int x) { return x % 2 == 0; });           // C++20: remove matching elements

// lazy pipeline (C++20 ranges), a bit like a Python generator expression
for (int x : v | std::views::filter([](int x) { return x > 2; })
               | std::views::transform([](int x) { return x * x; }))
    std::cout << x << ' ';

std::unordered_map<std::string, int> counts;
counts["apple"]++;                         // operator[] INSERTS a default (0) if missing
if (counts.contains("pear")) {}            // C++20; use this to check without inserting
for (const auto& [word, n] : counts) std::cout << word << "=" << n << "\n";   // structured bindings
```

**Gotchas:**

- `map[key]` inserts on read; use `.contains()`, `.find()` or `.at()` (throws if missing) when you only want to look.
- Modifying a vector (`push_back`, `erase`, `insert`) can invalidate iterators, pointers and references into it.
- Lambda captures: `[x]` copies, `[&x]` references. `[&]` capturing locals in a lambda that outlives the function is a dangling reference.
- `v[i]` doesn't bounds-check; `v.at(i)` does (throws `std::out_of_range`).

**Exercise 6:** Read a text file with `std::ifstream` and `std::getline`, count word frequencies in an `std::unordered_map<std::string, int>`, then copy the entries into a `std::vector<std::pair<std::string, int>>`, sort it by count descending with a lambda, and print the top 10. No raw loops allowed for the sorting or filtering.

## Module 7: Templates, errors and modern extras

Templates are compile-time generics: the compiler stamps out a separate version for each type you use. Because of that, **template definitions must live in the header**, not a `.cpp`, which is the most common "undefined reference" surprise.

```cpp
// function template
template <typename T>
T max_of(const T& a, const T& b) { return a > b ? a : b; }

// class template
template <typename T>
class Stack {
public:
    void push(T value) { data_.push_back(std::move(value)); }
    T pop() { T v = std::move(data_.back()); data_.pop_back(); return v; }
    bool empty() const { return data_.empty(); }
private:
    std::vector<T> data_;
};

// C++20 concepts: constrain what T can be (much clearer error messages)
#include <concepts>
template <typename T>
concept Numeric = std::integral<T> || std::floating_point<T>;

template <Numeric T>
T average(const std::vector<T>& v) { /* ... */ }

// shorthand
auto twice(std::integral auto x) { return x * 2; }
```

Template error messages can run to hundreds of lines. Read the **first** error and look for the line in your own file; the rest is usually noise.

**Error handling:**

- **Exceptions** are the standard mechanism: `throw std::runtime_error("msg");` and `try { ... } catch (const std::exception& e) { std::cerr << e.what(); }`. Always catch by `const&`. Thanks to RAII, destructors run as the exception unwinds.
- **`std::optional<T>`** for "might not have a value" (a failed lookup isn't exceptional).
- **`std::expected<T, E>`** (C++23, like Rust's `Result`) if your compiler has it.
- Mark functions that can't throw `noexcept`.

**Other modern bits worth knowing:**

- `std::string_view`: a cheap non-owning view of a string, good for read-only parameters. Never return one pointing into a local string.
- `std::span<T>`: the same idea for contiguous arrays or vectors.
- `std::variant<A, B>` with `std::visit`: a type-safe tagged union, handy for ASTs or message types.
- `[[nodiscard]]` on functions whose return value shouldn't be ignored.
- `std::format("{} scored {:.2f}", name, score)` (C++20; `std::print` in C++23) instead of chained `<<`.
- `std::thread`/`std::jthread`, `std::mutex`, `std::atomic` for concurrency, if the project needs it.

**Exercise 7:** Turn your `IntStack` from Module 2 into a header-only `Stack<T>` template, make `pop()` return `std::optional<T>` instead of throwing, and write a `sum_all` function constrained to `Numeric` types. Try calling `sum_all` on a `std::vector<std::string>` and read the concept error.

## Capstone: a command-line cricket scorer

Build `scorer`, a CMake project that reads ball-by-ball events from a file, keeps a live scorecard, and prints batting and bowling figures. It is small enough for a weekend but exercises every module: multiple headers, polymorphism with `unique_ptr`, STL containers and algorithms, RAII file handling, templates, and error handling.

**Input format** (`match.txt`, one ball per line):

```
BAT Smith Jones        # openers
BOWL Patel
1
4
W bowled               # wicket
BAT Brown
.                      # dot ball
WD                     # wide (1 extra, ball not counted)
6
OVER                   # next over
BOWL Khan
```

**Suggested structure:**

```
scorer/
├── CMakeLists.txt
├── include/
│   ├── player.hpp      # Batter / Bowler stats structs
│   ├── event.hpp       # abstract Event + Runs, Wicket, Extra, OverEnd subclasses
│   ├── parser.hpp      # line -> std::unique_ptr<Event>
│   ├── innings.hpp     # owns the state; applies events
│   └── table.hpp       # template helper for printing aligned tables
├── src/                # matching .cpp files + main.cpp
└── tests/
```

**Milestones** (tick them off as you go):

- [ ] **M1 (Modules 1–2):** CMake project builds; `main` opens the file given in `argv[1]` and echoes each line. Handle a missing file with a clear error.
- [ ] **M2 (Modules 3, 5):** `Batter` and `Bowler` classes with `const` getters. `Innings` stores them in `std::unordered_map<std::string, Batter>` and tracks who's on strike via a pointer or reference. Swap strike on odd runs and at the end of an over.
- [ ] **M3 (Module 4):** an abstract `Event` with `virtual void apply(Innings&) const = 0;`. The parser returns `std::unique_ptr<Event>`, and the innings is replayed from a `std::vector<std::unique_ptr<Event>>`.
- [ ] **M4 (Module 6):** print the scorecard sorted by runs (or batting order), strike rates, bowling economy, and the top scorer, using `std::ranges` algorithms rather than hand-written loops.
- [ ] **M5 (Module 7):** a `print_table<T>` template that takes rows and column accessor lambdas; the parser returns `std::optional` or throws a custom `ParseError` with the line number for malformed input.
- [ ] **M6:** an `undo` command that pops the last event and replays the innings from scratch, which is easy thanks to the event log.

**Stretch goals:** add unit tests with [Catch2](https://github.com/catchorg/Catch2) or GoogleTest via CMake's `FetchContent`; add a second innings and a result; run the whole thing under `valgrind` or the sanitizers and get it perfectly clean; replace the class hierarchy with `std::variant<Runs, Wicket, Extra, OverEnd>` and `std::visit`, and compare the two designs.

## Cheat sheet

Keep this open while working on the honours project.

| Symptom / question | Likely cause or answer |
| --- | --- |
| `undefined reference to X` | declared but not defined, `.cpp` missing from CMake, or template defined in a `.cpp` |
| `multiple definition of X` | non-`inline` function or global variable defined in a header |
| `X was not declared in this scope` | missing `#include`, missing `std::`, or used before declaration |
| crash / weird values | dangling pointer, uninitialised variable, out-of-bounds `[]`: rerun with `-fsanitize=address,undefined` |
| "passing const X as this discards qualifiers" | calling a non-`const` method on a `const` object: mark the method `const` |
| wall of template errors | read the first error only; find the line in your code |
| derived behaviour lost | object slicing (stored `Base` by value) or missing `virtual`/`override` |
| vector copies instead of moving | move constructor not `noexcept` |

**Defaults when in doubt:**

- Parameters: `const T&` for reading big things, `T` for small things, `T&` for outputs.
- Ownership: `std::unique_ptr` via `std::make_unique`; never raw `new`.
- Containers: `std::vector`, then `std::unordered_map`.
- Loops: `for (const auto& x : c)`; algorithms over hand-written loops.
- Classes: Rule of Zero; `const` methods; `explicit` single-argument constructors; `override` on overrides.
- Build: CMake, `-Wall -Wextra`, sanitizers in debug builds, treat warnings as bugs.

**Further reading:** [cppreference](https://en.cppreference.com) for lookups, [learncpp.com](https://www.learncpp.com) for any topic that needs a fuller explanation, and the [C++ Core Guidelines](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines) for style questions. For a single book, Stroustrup's *A Tour of C++* (3rd edition) is short and covers C++20.
