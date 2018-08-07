class: center
name: title
count: false

<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto">

# Why Rust?

.grey[Santiago Pastorino]

---

# About Me

- Computer Science at fing
- WyeWorks co-founder
- Ruby on Rails core member
- Rust NLL & wasm

<div style="height: 2rem"></div>

Contact:

- spastorino@gmail.com

---

# Agenda

1. Systems Programming
1. What is Rust?
1. Why Rust?
1. Use cases
1. Ecosystem & Community

---

# Systems Programming

Systems programming aims to produce software and software platforms which provide **services to other software**, are **performance constrained**, or both.
(e.g. Operating Systems, Browsers, Game Engines, etc)

???

service to other software
performance constrained
OS, Browser

--

The primary distinguishing characteristic of systems programming when compared to application programming is that application programming aims to produce software which **provides services to the user directly** (e.g. word processor)

???

vs app programming
provides services to users

--

System programming requires a great degree of **hardware awareness**.

???

TODO: see more definitions

---

# Programming Languages

So many to choose from

C, C++, Java, Go, C#, Clojure, JavaScript, Python, Ruby

Most not suitable for systems development

---

# Programming Languages

So many to choose from

C, C++, Java, Go, C#, Clojure, ~~JavaScript~~, ~~Python~~, ~~Ruby~~

Most not suitable for systems development

- Hard to predict or poor performance

---

# Programming Languages

So many to choose from

C, C++, ~~Java~~, ~~Go~~, ~~C#~~, ~~Clojure~~, ~~JavaScript~~, ~~Python~~, ~~Ruby~~

Most not suitable for systems development

- Hard to predict or poor performance
- Reliance on hard to manage runtime machinery e.g. "garbage collection"
  or atomic ref-counting

---

# Programming Languages

So many to choose from

C, C++, ~~Java~~, ~~Go~~, ~~C#~~, ~~Clojure~~, ~~JavaScript~~, ~~Python~~, ~~Ruby~~

Most not suitable for systems development

- Hard to predict or poor performance
- Reliance on hard to manage runtime machinery e.g. "garbage collection"
  or atomic ref-counting

... but the languages remaining are unsafe ...
- bugs might crash application, corrupt data, exposure to "pwnage"

--

... and complicate utilization of available (multicore) parallelism.

---

# Programming Languages

<img src="content/images/rust-meetup-languages-decision-1.png" alt="Desicions 1">

---

# Programming Languages

<img src="content/images/rust-meetup-languages-decision-2.png" alt="Desicions 2">

---

<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto" style="position: absolute; right: 0rem; margin-top: -2rem;">

# What is Rust?

- "New" systems programming language
  - 1.0 released in 2015

--
- Multiparadigm 
  - Imperative, Structured, Functional, Concurrent, Generic, Compiled 

--
- Static strong Typing
  - Inference

--
- Emphasizing control, safety, and speed

--
- Most loved programming language (2016, 2017 & 2018)

???

The type safety of Haskell, the concurrency of Erlang, and the speed of C++

---

<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto" style="position: absolute; right: 0rem; margin-top: -2rem;">

# Why use Rust?

- Abstraction without overhead
- Memory safety without garbage collection
- Concurrency without data races

--

Provides the ability to **hack without fear**.

---

# Why should I care?

- Experienced C++ hacker?
  - Make **and maintain** the designs you always wanted and prevent
    nasty bugs
- Prefer Ruby? JavaScript?
  - Tune up your application and address hot-spots. Lower memory usage.
    Add threads without fear.
- Web assembly

---

# Why use Rust?

- **Abstraction without overhead**
- Memory safety without garbage collection
- Concurrency without data races

---

# Abstraction without overhead

- High-level code
  - Algebraic data types
  - Generics
  - Traits
  - Closures
  - High order functions
  - Higienic macros
  - Testing built in
- Low-level performance
  - Fast code
  - Low memory footprint
  - with zero cost (no GC, unboxed closures, monomorphization); no runtime
- Cross-lang interop

???

- Monomorphization is a compilation strategy to allow polymorphism with static dispatch
- Monomorphization means generating specialized versions of generic functions

- boxed closures: current closures in Rust are "boxed" in that they consist of a function pointer, and a pointer to the closure environment (which contains captured variables). LLVM has trouble inlining and optimising around these indirections.
- Unboxed closures work by having each closure expand to an anonymous type which is effectively a struct that contains the captured variables, and implements one of the three kinds of "call" operator.

- Traits as interfaces
- Traits for code reuse
- Traits for operator overloading
- Trait objects

---

# Zero-cost abstractions

```rust
enum Event {
    Load,
    KeyPress(char),
    Click { x: i64, y: i64 }
}

fn print_event(event: Event) {
    match event {
        Event::Load => println!("Loaded"),
        Event::KeyPress(c) => println!("Key {} pressed", c),
        Event::Click {x, y} => println!("Clicked at x={}, y={}", x, y),
    }
}
```

???

Algebraic data types
Enum variants, Tuple Struct and Struct
Pattern matching
Macros

---

# Zero-cost abstractions

```rust
fn is_whitespace(text: &str) -> bool {
    text.chars()
        .all(|c| c.is_whitespace())
}
```

```rust
fn load_images(paths: &[PathBuf]) -> Vec<Image> {
    paths.iter()
         .map(|path| Image::load(path))
         .collect()
}
```

---

# Generics

```rust
enum Option<T> {
  Some(T),
  None,
}
```

???

There's no nulls also

The interesting thing about this to me is Option is very much a core feature of Rust, and one of the first features you will probably learn about, and yet for it to even exist it requires both generics and sum types. It’s used ubiquitously throughout the Rust standard library wherever you might otherwise use null, a language feature criticized by its own creator Tony Hoare as a “billion dollar mistake”.

---

# Generics

```rust
enum Option<T> {
  Some(T),
  None,
}

fn unwrap_or<T>(opt: Option<T>, default: T) -> T {
  match opt {
    Some(t) => t,
    None => default,
  }
}
```

---

# Generics

```rust
enum Option<T> {
  Some(T),
  None,
}

impl<T> Option<T> {
  fn unwrap_or(self, def: T) -> T {
    match self {
      Some(t) => t,
      None => def,
    }
  }
}
```

---

# Traits

```rust
trait Print {
  fn print(&self);
}

impl Print for u64 {
  fn print(&self) { println!(“{}”, self) }
}

impl Print for char {
  fn print(&self) { println!(“‘{}’”, self) }
}
```

???

Traits are interfaces

---

# Traits

```rust
fn main() {
  let v1: u64 = 0;
  v1.print();

  let v2: char = 'h';
  v2.print();
}
```

---

# Traits for reuse: default methods

```rust
trait Read {
  fn read(&mut self, buf: &mut [u8])
          -> Result<usize>;

  fn read_to_end(&mut self, buf: &mut Vec<u8>)
                 -> Result<usize> {
    // generic implementation
  }

  // additional default methods:
  // read_to_string, read_exact, by_ref, bytes,
  // chars, chain, take
}
```

---

# Traits for reuse: default methods

```rust
impl Read for File {
  fn read(&mut self, buf: &mut [u8])
          -> Result<usize> { ... }
}

fn read_file(f: &File) -> String {
   let mut contents = String::new();
   f.read_to_string(&mut contents).unwrap();
   contents
}
```

---

# Traits for reuse: layering implementations

```rust
trait Clone {
  fn clone(&self) -> Self;
}

impl<T: Clone, U: Clone> Clone for (T, U) {
  fn clone(&self) -> (T, U) {
    (t.clone(), u.clone())
  }
}

impl<T: Clone> Clone for Vec<T> { ... }
```

---

# Traits for operator overloading

```rust
struct Item {
  name: &’static str,
  price: f32,
}

impl PartialEq for Item {
  fn eq(&self, other: &Item) -> bool {
    self.name == other.name &&
      self.price == other.price
  }
}
```

---

# Derive Trait implementations

```rust
#[derive(PartialEq)]
struct Item {
  name: &’static str,
  price: f32,
}
```

---

# High-level code, low-level performance

Let's compare and contrast a **Ruby on Rails** method implemented in pure
**Ruby** and as a native extension in **C** and in **Rust**.

---

# Ruby blank?

```ruby
class String
  def blank?
    /\A[[:space:]]*\z/ == self
  end
end
```

---

# C blank?

```c
static VALUE
rb_str_blank_as(VALUE str)
{
  rb_encoding *enc;
  char *s, *e;

  enc = STR_ENC_GET(str);
  s = RSTRING_PTR(str);
  if (!s || RSTRING_LEN(str) == 0) return Qtrue;

  e = RSTRING_END(str);
  while (s < e) {
    int n;
    unsigned int cc = rb_enc_codepoint_len(s, e, &n, enc);

    switch (cc) {
      case 9:
      case 0xa:
      case 0xb:
```

???

95 lines of code

---

# C blank? (part 2)

```c
      case 0xc:
      case 0xd:
      case 0x20:
      case 0x85:
      case 0xa0:
      case 0x1680:
      case 0x2000:
      case 0x2001:
      case 0x2002:
      case 0x2003:
      case 0x2004:
      case 0x2005:
      case 0x2006:
      case 0x2007:
      case 0x2008:
      case 0x2009:
      case 0x200a:
      case 0x2028:
```

---

# C blank? (part 3)

```c
      case 0x2029:
      case 0x202f:
      case 0x205f:
      case 0x3000:
#if ruby_version_before_2_2()
      case 0x180e:
#endif
          /* found */
          break;
      default:
          return Qfalse;
    }
    s += n;
  }
  return Qtrue;
}
```

---

# C blank? (part 4)

```c
static VALUE
rb_str_blank(VALUE str)
{
  rb_encoding *enc;
  char *s, *e;

  enc = STR_ENC_GET(str);
  s = RSTRING_PTR(str);
  if (!s || RSTRING_LEN(str) == 0) return Qtrue;

  e = RSTRING_END(str);
  while (s < e) {
    int n;
    unsigned int cc = rb_enc_codepoint_len(s, e, &n, enc);

    if (!rb_isspace(cc) && cc != 0) return Qfalse;
    s += n;
  }
  return Qtrue;
}
```

---

# Rust blank?

```rust
extern “C” fn fast_blank(buf: Buf) -> bool {
    buf.as_slice().chars().all(|c| c.is_whitespace())
}
```

---

# blank? performance

<img src="content/images/performance.png" alt="Performance">

---

<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto" style="position: absolute; right: 0rem; margin-top: -2rem;">

# Why use Rust?

- Abstraction without overhead
- **Memory safety without garbage collection**
- Concurrency without data races

---

# Memory safety without garbage collection

- No segmentation fauls
- No undefined behavior
- No double free
- No dangling pointers
- No iterator invalidation
- No buffer overflows
- No null pointers
- No data races
- Guaranteed by Rust's ownership system at compile time

---

# In C

- Array capacity is not checked on access
    - Easy to get buffer overflows
- Every `malloc` needs exactly one `free`
    - Easy to get _use-after-free_ or _double-free_ bugs

Vulnerabilities caused by memory unsafety are still common

???

There are a lot of more issues.

---

# Memory Safety

<img alt="Buffer Overflow Vulnerabilities in Linux" src="content/images/Buffer Overflow Vulnerabilities in Linux.svg" style="margin-top: 0rem; margin-bottom: -2rem;">

<img src="content/images/Tux.svg" alt="Linux logo" width="120rem" height="auto" style="display:block; position: absolute; top: 1rem; right: 3rem;">

.grey[.small[Source: https://www.cvedetails.com/product/47/Linux-Linux-Kernel.html?vendor_id=33]]

???

.grey[
- CVE = Common Vulnerabilities and Exposures
]

---

# Memory Safety

<img alt="Linux CVEs in 2018" src="content/images/Linux CVEs in 2018.svg" style="margin-top: 0rem; margin-bottom: -2rem;">

<img src="content/images/Tux.svg" alt="Linux logo" width="120rem" height="auto" style="display:block; position: absolute; top: 1rem; right: 3rem;">

.grey[.smaller[Source: https://www.cvedetails.com/vulnerability-list/vendor_id-33/product_id-47/year-2018/Linux-Linux-Kernel.html]]


???

.grey[
- CVE = Common Vulnerabilities and Exposures
]

---

# "Manual" memory management in Rust:

- Values **owned** by creator.
- Values **moved** via assignment.
- When final owner returns, **value is freed**.

All this feels invisible and prevents _double free_ errors.

???

Move semantics

RAII (Resource Acquisition Is Initialization)

Variables in Rust do more than just hold data in the stack, they can also own resources, e.g. Box<T> owns memory in the heap. Because Rust enforces the RAII discipline, whenever an object goes out of scope, its destructor is called and the resources owned by it are freed. This behavior shields against resource leak bugs.

---

# Ownership

```rust
fn main() {
    let apple = Apple::new();
    eat(apple); // Give ownership of the apple.
    eat(apple); // Error: `apple` has been moved.
}

/// eat function takes ownership of the apple
fn eat(apple: Apple) {
}
```

---

# Ownership

```rust
fn main() {
    let apple = Apple::new();
    let mut bag = Vec::new();
    bag.push(apple); // Give ownership
    bag.push(Apple::new());
    deliver(bag); // Give ownership of bag and it's contents
}

/// deliver function takes ownership
/// of the vector
fn deliver(bag: Vec<Apple>) {
    // ...
}
```

???

You can't use after move, if you need that

---

# Ownership

<img src="content/images/rust-meetup-children-ownership-1r.png" alt="Ownership 1" width="300rem" height="auto" style="position: absolute; right: 3rem; margin-top: 0rem">

```rust
fn main() {
*   let apple = Apple::new();
    let mut bag = Vec::new();
    bag.push(apple); // Give ownership
    bag.push(Apple::new());
    deliver(bag); // Give ownership of bag and it's contents
}

/// deliver function takes ownership
/// of the vector
fn deliver(bag: Vec<Apple>) {
    // ...
}
```

---

# Ownership

<img src="content/images/rust-meetup-children-ownership-2r.png" alt="Ownership 2" width="300rem" height="auto" style="position: absolute; right: 3rem; margin-top: 0rem">

```rust
fn main() {
    let apple = Apple::new();
*   let mut bag = Vec::new();
    bag.push(apple); // Give ownership
    bag.push(Apple::new());
    deliver(bag); // Give ownership of bag and it's contents
}

/// deliver function takes ownership
/// of the vector
fn deliver(bag: Vec<Apple>) {
    // ...
}
```

---

# Ownership

<img src="content/images/rust-meetup-children-ownership-3r.png" alt="Ownership 3" width="300rem" height="auto" style="position: absolute; right: 3rem; margin-top: 0rem">

```rust
fn main() {
    let apple = Apple::new();
    let mut bag = Vec::new();
*   bag.push(apple); // Give ownership
    bag.push(Apple::new());
    deliver(bag); // Give ownership of bag and it's contents
}

/// deliver function takes ownership
/// of the vector
fn deliver(bag: Vec<Apple>) {
    // ...
}
```

---

# Ownership

<img src="content/images/rust-meetup-children-ownership-4r.png" alt="Ownership 4" width="300rem" height="auto" style="position: absolute; right: 3rem; margin-top: 0rem">

```rust
fn main() {
    let apple = Apple::new();
    let mut bag = Vec::new();
    bag.push(apple); // Give ownership
*   bag.push(Apple::new());
    deliver(bag); // Give ownership of bag and it's contents
}

/// deliver function takes ownership
/// of the vector
fn deliver(bag: Vec<Apple>) {
    // ...
}
```

---

# Ownership

<img src="content/images/rust-meetup-children-ownership-6r.png" alt="Ownership 6" width="300rem" height="auto" style="position: absolute; right: 3rem; margin-top: 0rem">

```rust
fn main() {
    let apple = Apple::new();
    let mut bag = Vec::new();
    bag.push(apple); // Give ownership
    bag.push(Apple::new());
*   deliver(bag); // Give ownership of bag and it's contents
}

/// deliver function takes ownership
/// of the vector
fn deliver(bag: Vec<Apple>) {
    // ...
}
```

---

# Borrowing

<img src="content/images/rust-meetup-children-borrowing-0r.png" alt="Borrowing" width="300rem" height="auto" style="position: absolute; right: 3rem; margin-top: 0rem">

```rust
fn main() {
    let apple = Apple::new();
    let mut bag = Vec::new();
    bag.push(apple);
    bag.push(Apple::new());
    let weight = weigh(&bag); // Loan out the bag
}

/// weigh function takes a shared
/// reference to the vector
fn weigh(bag: &Vec<Apple>) -> u32 {
    // ...
}
```

---

# Mutable Borrowing

<img src="content/images/rust-meetup-children-borrowing-0r.png" alt="Borrowing" width="300rem" height="auto" style="position: absolute; right: 3rem; margin-top: 0rem">

```rust
fn main() {
    let apple = Apple::new();
    let mut bag = Vec::new();
    bag.push(apple);
    bag.push(Apple::new());
    deliver(&mut bag); // Loan out the bag for mutation
}

/// deliver function takes a mutable shared
/// reference to the vector
fn deliver(bag: &mut Vec<Apple>) {
    // mutate the bag
}
```

---

# Dangers of mutation

```rust
let mut buffer: String = format!("Hello");
let slice = &buffer[1..];
buffer.push_str(" World");
println!("{:?}", slice);
```

---

# Dangers of mutation

```rust
*let mut buffer: String = format!("Hello");
let slice = &buffer[1..];
buffer.push_str(" World");
println!("{:?}", slice);
```

<img src="content/images/rust-meetup-mutation-1r.png" alt="Mutation 1">

---

# Dangers of mutation

```rust
let mut buffer: String = format!("Hello");
*let slice = &buffer[1..];
buffer.push_str(" World");
println!("{:?}", slice);
```

<img src="content/images/rust-meetup-mutation-2r.png" alt="Mutation 2">

---

# Dangers of mutation

```rust
let mut buffer: String = format!("Hello");
let slice = &buffer[1..];
*buffer.push_str(" World");
println!("{:?}", slice);
```

<img src="content/images/rust-meetup-mutation-3r.png" alt="Mutation 3">

---

# Dangers of mutation

```rust
let mut buffer: String = format!("Hello");
let slice = &buffer[1..];
*buffer.push_str(" World");
println!("{:?}", slice);
```

<img src="content/images/rust-meetup-mutation-4r.png" alt="Mutation 4">

---

# Dangers of mutation

```rust
let mut buffer: String = format!("Hello");
let slice = &buffer[1..];
*buffer.push_str(" World");
println!("{:?}", slice);
```

<img src="content/images/rust-meetup-mutation-5r.png" alt="Mutation 5">

---

# Dangers of mutation

```rust
let mut buffer: String = format!("Hello");
let slice = &buffer[1..];
*buffer.push_str(" World");
println!("{:?}", slice);
```

<img src="content/images/rust-meetup-mutation-6r.png" alt="Mutation 6">

---

# Rust solution

Compile-time read-write-lock:

Creating a shared reference to X “read locks” X.
- Other readers OK.
- No writers.
- Lock lasts until reference goes out of scope.

--

Creating a mutable reference to X “writes locks” X.
- No other readers or writers.
- Lock lasts until reference goes out of scope.

Never have a reader/writer at same time.

---

# Sharing "freezes" data (temporarily)

```rust
let mut bag = Vec::new();
bag.push(...);     // `bag` **mutable** here
let r = &bag;      // `bag` **borrowed** here
bag.len();         // reading `bag` ok while shared
bag.push(...);     // cannot mutate while shared
r.push(...);       // cannot mutate through a shared ref
                   // `bag` borrow ends here
bag.push(...);     // after last use of `r`, `bag` is mutable again
```

---

# Mutable references: no other access to data

```rust
let mut bag = Vec::new();
bag.push(...);     // `bag` **mutable** here
let r = &mut bag;  // `bag` **mutably borrowed** here
bag.len();         // cannot access `bag` while mutably borrowed
r.push(...);       // but can mutate through `r`
                   // `bag` borrow ends here
bag.push(...);     // after last use of `r`, `bag` is accessible again
```

---

# Ownership and Borrowing

|Type    |Ownership          |Alias?|Mutate?|
|--------|-------------------|------|-------|
| T      | Owner             |      | y     |
| &T     | Shared reference  | y    |       |
| &mut T | Mutable reference |      | y     |

---

# Borrowing and Lifetimes

```rust
let mut buffer: String = format!("Hello");
let slice = &buffer[1..];   // `'l` starts and borrow locks `buffer` for
                            // lifetime `'l` of resulting reference
buffer.push_str(" World");  // error can not borrow mutably while borrowed immutably
println!(“{:?}”, slice);
```

**Rule**: No mutation during **lifetime of borrow**.

**Lifetime**: span of code where reference is used.

---

# Borrowing and Lifetimes

```rust
fn main() {
    let mut buffer: String = format!("Hello");

    for i in 0 .. buffer.len() {
        let slice = &buffer[i..];   // Borrow locks `buffer` until `slice`
                                    // goes out of scope
        buffer.push_str(" World");  // error: can not borrow mutably
                                    // while borrowed immutably
        println!(“{:?}”, slice);
    }

    buffer.push_str(" World");      // ok: `buffer` is not borrowed here
}
```

---

# Memory Safety: A Strict Compiler

- It can take some time until your program compiles
- Lifetimes can be complicated
    - “error: `x` does not live long enough”


However:
- “If it compiles, it usually works”
- Far less debugging
    - No data races!
- Refactoring is safe and painless

---

<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto" style="position: absolute; right: 0rem; margin-top: -2rem;">

# Why use Rust?

- Abstraction without overhead
- Memory safety without garbage collection
- **Concurrency without data races**

---

# Concurrency without data races

- Multiparadigm concurrency
  - msg passing via channels
  - shared state (R/W- capabilities controlled via types)
  - use native threads... or scoped threads ... or work-stealing ...

---

# Data Races

<table style="border-bottom-style: none; border-top-style: none;">
    <tbody>
        <tr>
            <td width="22%">&nbsp;&nbsp;&nbsp;Sharing</td>
	    <td>Actor-based lenguages</td>
        </tr>
        <tr>
            <td>+ Mutation</td>
	    <td>Functional languages</td>
        </tr>
        <tr>
            <td>+ No ordering</td>
	    <td>Sequential programming</td>
        </tr>
        <tr>
            <td style="border-bottom-style: solid"></td>
	    <td></td>
        </tr>
        <tr>
            <td>&nbsp;&nbsp;&nbsp;Data race</td>
	    <td></td>
        </tr>
    </tbody>
</table>

---

# Data Races


<table style="border-bottom-style: none; border-top-style: none;">
    <tbody>
        <tr>
            <td width="22%" style="border-top-style: solid; border-left-style: solid; border-right-style: solid;">&nbsp;&nbsp;&nbsp;Sharing</td>
	    <td>Rust: no sharing and mutation</td>
	    <td></td>
        </tr>
        <tr>
            <td style="border-bottom-style: solid; border-left-style: solid; border-right-style: solid;">+ Mutation</td>
	    <td>at the same time</td>
	    <td></td>
        </tr>
        <tr>
            <td>+ No ordering</td>
	    <td></td>
	    <td></td>
        </tr>
        <tr>
            <td style="border-bottom-style: solid"></td>
	    <td></td>
	    <td></td>
        </tr>
        <tr>
            <td>&nbsp;&nbsp;&nbsp;Data race</td>
	    <td></td>
	    <td></td>
        </tr>
    </tbody>
</table>

---

# Parallelism

Observation:

- Building parallel abstractions is easy.
- Misusing those abstractions is also easy.

```go
func foo(channel chan<- map[string]string) {
	m := make(map[string]string)
	m["Hello"] = "World"
	channel <- m              // send data over channel
	m["Hello"] = "Data Race"  // but how to stop sender from using
	                          // it afterwards?
}
```

---

# Parallelism

```rust
fn foo(channel: &mut Channel) {
  let m = HashMap::new();
  m.insert("Hello", "World");
  channel.send(m);
  m.insert("Hello", "Data Race"); // **Error**: use of moved value: `m`
}

impl<T> Channel<T> {
  // Takes ownership of the data
  fn send(&mut self, data: T) {
    // ...
  }
}
```

---

# Concurrency paradigms

| Paradigm        | Ownership? | Borrowing? |
|-----------------|------------|------------|
| Message passing |     y      |            |
| Fork join       |            |     y      |

???

Rust multiparadigm concurrency
message passing
mutable shared memory

---

# Parallelism

```rust
fn load_images(paths: &[PathBuf]) -> Vec<Image> {
    paths.iter() // For each path ...
         .map(|path| {
	     Image::load(path) // ... load an image ...
	 })
	 .collect() // ... create and return a vector.
}
```

--

```rust
extern crate rayon; // Third-party library

fn load_images(paths: &[PathBuf]) -> Vec<Image> {
    paths.par_iter() // Make it parallel
         .map(|path| {
	     Image::load(path)
	 })
	 .collect()
}
```

---

# Parallelism with mutability

```rust
fn load_images(paths: &[PathBuf]) -> Vec<Image> {
    let mut jpgs = 0; // How many jpgs seen so far?
    paths.par_iter() // Make it parallel
         .map(|path| {
            // If current file name ends in "jpg" ...
             if path.ends_with(".jpg") {
                 // multiple mutable borrows occurr here
                 jpgs += 1;
             }
             Image::load(path)
         })
         .collect()
}
```

---

# Parallelism with mutability

```rust
fn load_images(paths: &[PathBuf]) -> Vec<Image> {
    let mut jpgs = 0; // How many jpgs seen so far?
    paths.par_iter() // Make it parallel
         .map(|path| {
            // If current file name ends in "jpg" ...
             if path.ends_with(".jpg") {
                 // multiple mutable borrows occurr here
                 jpgs += 1;
             }
             Image::load(path)
         })
         .collect()
}
```

Rust prevents a data race at compile time.

---

# A Powerful Type System: Mutexes

<table>
    <thead><tr><th width="50%" style="text-align: center">C++</th><th width="50%">Rust</th></tr></thead>
    <tbody>
        <tr>
            <td>
<pre><code class="C++">std::vector<int> data = {1, 2, 3};
// mutex is unrelated to data
std::mutex mutex;

// unsynchronized access possible
data.push_back(4);

mutex.lock();
data.push_back(5);
mutex.unlock();
</pre></code>
            </td><td>
<pre><code class="Rust">let data = vec![1, 2, 3];
// mutex owns data
let mutex = Mutex::new(data);

// compilation error: data was moved
data.push(4);

let mut d = mutex.lock().unwrap();
d.push(5);
// released at end of scope
</pre></code>
            </td>
        </tr>
    </tbody>
</table>

⇒ Rust ensures that Mutex is locked before accessing data

---

# A Powerful Type System

Allows to:

- Make misuse impossible
.grey[- Impossible to access data behind a Mutex without locking]
- Represent contracts in code instead of documentation
.grey[
- Page size of page and frame parameters must match in `map_to`
]

<div style="height:1rem"></div>

Everything happens at compile time ⇒ _No run-time cost!_

---

# Concurrency paradigms

| Paradigm        | Ownership? | Borrowing? |
|-----------------|------------|------------|
| Message passing |     y      |            |
| Fork join       |            |     y      |
| Locking         |     y      |     y      |
| Lock-free       |     y      |     y      |
| Futures         |     y      |     y      |

---

class: center

# Who is using Rust?

<div>
  <img src="content/images/firefox.svg" alt="Firefox logo" width="150rem" height="auto">
  <img src="content/images/servo.png" alt="Firefox logo" width="150rem" height="auto">
</div>
<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="200rem" height="auto">


---

# Who is using Rust?

- **Amazon** - Building tools in Rust.
- **Atlassian** (makers of Jira) - Using Rust in the backend.
- **Dropbox** - Using Rust in both the frontend and backend.
- **Facebook** - Tools for source control.
- **Google** - As part of the Fuchsia project.
- **Microsoft** - Using Rust in part of their new Azure IoT work.
- **npm** - Using Rust in some of the npm core services.
- **Red Hat** - Creating a new storage system
- **Reddit** - Using Rust in its comment processing
- **Twitter** - As part of the build team support for Twitter.

You can see even more on the Friends of Rust that include other familiar names like **Baidu**, **Wire**, **Mozilla**, **Samsung**, **Cloudflare**, **Chef**, **Canonical**, **Coursera**, **Tor** and more.

---

# Who is using Rust?

**Redox OS**: Most complete Rust OS, microkernel design

<img class="center" alt="Screenshot of Redox running a webbrowser and a file manager" src="content/images/redox-screenshot.png" style="margin-left: auto; margin-right: auto; width: auto; height: 25rem;">

---

# Easy Dependency Management

.float-right[![Cargo logo](content/images/cargo-logo.png)]

- Over 15000 crates on **crates.io**
- Simply specify the desired version
.grey[    - Add single line to `Cargo.toml`]
- Cargo takes care of the rest
.grey[    - Downloading, building, linking]

---

# Great Tooling

- **rustup**: Use multiple Rust versions for different directories
- **cargo**: Automatically download, build, and link dependencies
- **rustfmt**: Format Rust code according to style guidelines
--

- **Rust Playground**: Run and share code snippets in your browser

![Rust Playground screenshot](content/images/playground.png)

---

# Great Tooling

- **clippy**: Additional warnings for dangerous or unidiomatic code

```rust
fn equal(x: f32, y: f32) -> bool {
    if x == y { true } else { false }
}
```
--

```
error: `strict comparison of f32 or f64`
 --> src/main.rs:2:8
  |
2 | if x == y { true } else { false }
  |    ^^^^^^ help: `consider comparing them within some error: (x - y).abs() < err`

warning: `this if-then-else expression returns a bool literal`
 --> src/main.rs:2:5
  |
2 | if x == y { true } else { false }
  | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^ help: `you can reduce it to: x == y`
```

---

# Great Tooling

- **proptest**: A property testing framework

```rust
fn parse_date(s: &str) -> Option<(u32, u32, u32)> {
    // […] check if valid YYYY-MM-DD format
    let year = &s[0..4];
    let month = &s[`6`..7]; // BUG: should be 5..7
    let day = &s[8..10];
    convert_to_u32(year, month, date)
}
proptest! {
    #[test]
    fn parse_date(`y in 0u32..10000`, `m in 1u32..13`, `d in 1u32..32`) {
        let date_str = format!("{:04}-{:02}-{:02}", y, m, d);
        let (y2, m2, d2) = parse_date(&date_str).unwrap();
        prop_assert_eq!((y, m, d), (y2, m2, d2));
    }
}
```

---

<pre style="margin-left: 2rem;"><code style="line-height: 0.9; font-size: 20px;">
- try random values                     y = 2497, m = 8, d = 27     passes
    |                                   y = 9641, m = 8, d = 18     passes
    | (failed test case found)          `y = 7360, m = 12, d = 20`    fails

- reduce y to find simpler case         y = 3680, m = 12, d = 20    fails
    |                                   y = 1840, m = 12, d = 20    fails
    |                                   y = 920, m = 12, d = 20     fails
    |                                   y = 460, m = 12, d = 20     fails
    |                                   y = 230, m = 12, d = 20     fails
    |                                   y = 115, m = 12, d = 20     fails
    |                                   y = 57, m = 12, d = 20      fails
    |                                   y = 28, m = 12, d = 20      fails
    |                                   y = 14, m = 12, d = 20      fails
    |                                   y = 7, m = 12, d = 20       fails
    |                                   y = 3, m = 12, d = 20       fails
    |                                   y = 1, m = 12, d = 20       fails
    | (simplest y case still fails)     `y = 0, m = 12, d = 20`       fails

- reduce m to find simpler case         y = 0, m = 6, d = 20        passes
    |                                   y = 0, m = 9, d = 20        passes
    |                                   y = 0, m = 11, d = 20       fails
    | (minimum failure value found)     `y = 0, m = 10, d = 20`       fails

- reduce d to find simpler case         y = 0, m = 10, d = 10       fails
    |                                   y = 0, m = 10, d = 5        fails
    |                                   y = 0, m = 10, d = 3        fails
    |                                   y = 0, m = 10, d = 2        fails
    | (reduced test case found)         `y = 0, m = 10, d = 1`        fails
</code></pre>

.grey[.small[See <https://github.com/altsysrq/proptest>]]

---

# An Awesome Community

- Code of Conduct from the beginning
    - “We are committed to providing a **friendly, safe and welcoming environment** for all […]”
    - “We will exclude you from interaction if you insult, demean or harass anyone”
    - Followed on GitHub, IRC, the Rust subreddit, etc.
--
- It works!
    - No inappropriate comments in chats so far
    - Focused technical discussions

--

<div style="height: 1rem"></div>

**_vs_**:

> “So this patch is utter and absolute garbage, and should be shot in the
head and buried very very deep.”

<div class="right small grey" style="margin-top: -3rem;"><a href="https://lkml.org/lkml/2017/8/14/698">Linus Torvalds on 14 Aug 2017</a></div>

---

# No Elitism

- It doesn't matter where you come from
    - C, C++, Java, Python, JavaScript, …
- It's fine to ask questions
    - People are happy to help

