class: center
name: title
count: false

<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto">

# Why Rust?

.grey[Santiago Pastorino]

.grey[.smaller[WyeWorks co-founder | Rust compiler and types team member]]

---

<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto" style="position: absolute; right: 0rem; margin-top: -2rem;">

# Objectives

- **What is Rust?**
- Who is using Rust?
- What are Rust use cases?
- Why people love Rust?

---

<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto" style="position: absolute; right: 0rem; margin-top: -2rem;">

# What is Rust?

- Modern & safe systems programming language
  - Originally developed by Mozilla research
  - v1.0 released in 2015
- Emphasizing performance, type safety, and concurrency
- Multiparadigm
  - Ideas from FP, immutability, higher-order functions, algebraic data types, and pattern matching.
  - Also supports OOP via structs, enums, traits, and methods.
- Compiled, powerful type system, statically typed, type inference, generics
- Free and open-source software, MIT License or Apache License 2.0

???

- Mozilla research -> Firefox and Servo
- Safety without GC, all references point to valid memory, Borrow Checker
- Multiparadigm, influenced by functional programming
- Type inference, almost never write types. Only for definitions. Local vs Global Inference, Stability and explicit contracts APIs, Generics, Error messages, compiler complexity, etc

---

<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto" style="position: absolute; right: 0rem; margin-top: -2rem;">

# Objectives

- What is Rust?
- **Who is using Rust?**
- What are Rust use cases?
- Why people love Rust?

---

# Who is using Rust?

- **Linux Kernel** - Rust for Linux.
- **Google** - Android, Linux Drivers, cloud services, Fuchsia OS, etc.
- **Amazon** - S3, EC2, Firecracker, Bottlerocket OS, Aurora DSQL, CloudFront, DynamoDB, Lambda.
- **Microsoft** – Rust for Windows components, device drivers, and parts of Azure for memory safety.
- **Meta (Facebook)** – uses Rust in backend services. Libra, Mononoke, Mercurial and HHVM.
- **Mozilla** - Firefox rendering engine, Servo, Quantum, Stylo, WebRender.

Also **Cloudflare**, **Arm**, **Red Hat**, **Dropbox**, **Discord**, **Deno**, **npm**, **uv**, **sudo-rs**, **rustls**, and many more.

???

- Linux Kernel: Memory Safety, safer device drivers (often written by venders and common source of crashes)
- Google: Android, Linux Kernel drivers for Android Linux Stack, Performance critical and security sensitive infraestructure components. Fuchsia new OS microkernel for embedded and personal computers.
- Amazon: AWS Infraestructure. Firecracker (the microVM behind Lambda and Fargate), Bottlerocket OS (Linux based contained host US), Aurora DSQL (Fastest serverless distributed SQL database).
- Servo a parallel designed for both application and embedded use and aimsto achieve parallelism, security, modularity, and performance.
- Stylo integrate Servo's CSS style system into Gecko
- WebRender A GPU-based renderer for the web, render backend for Servo
- crosvm es un Virtual Machine Monitor / hipervisor
- Libra blockchain digital currency
- Mononoke and Mercurial, Mercurial server and client
- HHVM virtual machine to execute hack and php programs
- Firecracker virtualization technology for serverless computing
- https://x.com/letsencrypt/status/1314554154334007299
- https://x.com/ProssimoISRG/status/1473354582306742273
- https://x.com/nadavrot/status/1552324447029186560
- https://x.com/spastorino/status/1572715167598923776
- https://x.com/dwizzzleMSFT/status/1720134540822520268
- https://x.com/spastorino/status/1773025016822497392
- https://x.com/spastorino/status/1773766846723842186

---

<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto" style="position: absolute; right: 0rem; margin-top: -2rem;">

# Objectives

- What is Rust?
- Who is using Rust?
- **What are Rust use cases?**
- Why people love Rust?

---

# What are Rust use cases?

- Systems Programming
  - Operating systems & kernels (Linux drivers, Redox OS, Tock OS)
  - Virtualization & containers (AWS Firecracker, Cloud Hypervisor, Youki)
  - Compilers & runtimes (rustc, Cranelift, Wasmtime, Wasmer)
  - Databases & storage engines (TiKV, sled, Materialize)
  - Browsers & rendering engines (Firefox components, Servo)
  - Embedded firmware & device drivers
- Cloud & Infrastructure
  - Cloud platforms (AWS, Azure, Google/Android)
  - Networking stacks (TLS, QUIC, proxies like linkerd2)
  - Infrastructure tooling (Terraform providers, Kubernetes components, Krustlet)

---

# What are Rust use cases?

- Application Development
  - Web services & high-performance APIs (Actix, Axum, Warp)
  - Command-line tools (ripgrep, fd, bat, starship)
  - Game development (Bevy, Amethyst, macroquad)
  - Desktop & GUI apps (Tauri, Dioxus, egui)
- Specialized Domains
  - WebAssembly (frontend + edge computing, Deno, Wasmtime)
  - Blockchain & smart contracts (Solana, Polkadot/Substrate, NEAR)
  - Data science & ML/AI (Polars, ndarray, Rust ML ecosystem)
  - Scientific computing & HPC (simulation, numerical libraries)
  - Audio, video, & multimedia (Symphonia, GStreamer bindings)

---

# What are Rust use cases?

- Safety-Critical & Industry Applications
  - Robotics & automation (ROS2 integration, drones, satellites)
  - Automotive & aerospace software (embedded control, real-time systems)
  - Health & medical devices (where safety + reliability matter)
  - Financial services & fintech (low-latency trading, secure systems)

---

# People love Rust (2016 - ?)

.center[
<img src="content/images/most-loved-2016.png" alt="Stackoverflow Survey">
]

---

# People love Rust (2016 - 2025)

.center[
<img src="content/images/most-loved-2025.png" alt="Stackoverflow Survey">
]

---

<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto" style="position: absolute; right: 0rem; margin-top: -2rem;">

# Objectives

- What is Rust?
- Who is using Rust?
- What are Rust use cases?
- **Why people love Rust?**

---

<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto" style="position: absolute; right: 0rem; margin-top: -2rem;">

# Why people love Rust?

- **Performance**

---

# Performance

- Native machine code – no VM, no interpreter.
- No garbage collector – predictable performance.
- Zero-cost abstractions – modern features, no overhead.
- Efficient memory layout – cache-friendly, tightly packed.
- Static dispatch & inlining – generics compile to optimal code.
- Safe concurrency – parallelism without data races.
- Fine-grained control – drop to low-level when needed.

???

Runs as fast as C/C++ 
- Native machine code
  - optimized machine code via LLVM.
  - No virtual machine, interpreter, or bytecode layer.
- No garbage collector
  - Memory is managed at compile time through ownership and lifetimes.
  - Means predictable performance (no “stop-the-world” GC pauses).
- Zero-cost abstractions
  - High-level constructs (iterators, traits, async/await) compile away to the same low-level code you’d hand-write in C.
  - You get modern, expressive code without paying a performance penalty.
- Efficient memory layout
  - Control over structs, enums, and memory alignment.
  - Data is often cache-friendly and packed tightly, minimizing wasted memory and improving speed.
- Static dispatch & inlining
  - Generics and traits use monomorphization (like C++ templates).
  - Function calls can be inlined, avoiding runtime lookups.
  - Dynamic dispatch (via dyn Trait) is available, but only when you want it.
- Inlining & Optimizations
  - The compiler aggressively inlines functions.
  - Common patterns (pattern matching, Result/Option handling) become branchless machine instructions.
- Predictable Concurrency
  - Fearless concurrency: safe multithreading with no data races.
  - Async runtimes (like Tokio) handle millions of concurrent tasks efficiently.
- Fine-Grained Control
  - Like C/C++, you can drop down to unsafe code for ultimate control, but 99% of the time you stay in safe Rust.
  - Lets you optimize hot paths without compromising the rest of your system.
- Why not just use C(++) then?

---

<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto" style="position: absolute; right: 0rem; margin-top: -2rem;">

# Why people love Rust?

- Performance
- **Memory safety without GC**

---

# Memory safety

.center[
<img alt="Microsoft Memory Safety" src="content/images/microsoft-memory-safety-trends.png" style="margin-top: 0rem; margin-bottom: -2rem;">
]

.center[.grey[.smaller[Source: https://www.zdnet.com/article/microsoft-70-percent-of-all-security-bugs-are-memory-safety-issues/]]]


???

70% of all security bugs are memory safety issues

---

# Memory safety

.center[
<img alt="Greg KH Memory Safety" src="content/images/gregkh.png" style="margin-top: 0rem; margin-bottom: -2rem;">
]

.center[.grey[.smaller[Source: https://lore.kernel.org/rust-for-linux/2025021954-flaccid-pucker-f7d9@gregkh/]]]

???

Greg Kroah-Hartman is a major Linux kernel developer. As of April 2013, he is the Linux kernel maintainer for the -stable branch

---

# Memory safety

.center[
<img alt="te House Memory Safety" src="content/images/whitehouse.png" style="margin-top: 0rem; margin-bottom: -2rem;">
]

.center[.grey[.smaller[Source: https://bidenwhitehouse.archives.gov/oncd/briefing-room/2024/02/26/press-release-technical-report/]]]

???

Future Software should be memory safe and they specifically mention Rust.

---

# Memory safety

|                       | C/C++ |
| --------------------- | ----- |
| Control, flexibility  | 🎉    |
| Minimal to no runtime | 🎉    |
| Double free           | 😢    |
| Use after free        | 😢    |
| Data race             | 😢    |

---

# Memory safety

|                       | C/C++ | GC    |
| --------------------- | ----- | ----- |
| Control, flexibility  | 🎉    | 🤷‍♀️ |
| Minimal to no runtime | 🎉    | 🤷‍♀️ |
| Double free           | 😢    | 🎉    |
| Use after free        | 😢    | 🎉    |
| Data race             | 😢    | 😢    |

---

# Memory safety

|                       | C/C++ | GC    | Rust |
| --------------------- | ----- | ----- | ---- |
| Control, flexibility  | 🎉    | 🤷‍♀️ | 😎   |
| Minimal to no runtime | 🎉    | 🤷‍♀️ | 😎   |
| Double free           | 😢    | 🎉    | 😎   |
| Use after free        | 😢    | 🎉    | 😎   |
| Data race             | 😢    | 😢    | 😎   |

---

# Every language lets you give

```go
func foo() {
	gift := Gift { .. }
	channel <- gift
	gift.open()
}
```

<img src="content/images/gift1.jpg" alt="Gift 1" width="90%" style="margin-top: 0rem;">

???

What happens in most languages?

---

# Every language lets you give

```go
func foo() {
	`gift := Gift { .. }`
	channel <- gift
	gift.open()
}
```

<img src="content/images/gift2.jpg" alt="Gift 2" width="90%" style="margin-top: 0rem;">

---

# Every language lets you give

```go
func foo() {
	gift := Gift { .. }
	`channel <- gift`
	gift.open()
}
```

.col-right[
```go
// The other goroutine
gift := <- channel
gift.open()
```
]

<img src="content/images/gift3.jpg" alt="Gift 3" width="90%" style="margin-top: 0rem;">

---

# Every language lets you give

```go
func foo() {
	gift := Gift { .. }
	`channel <- gift`
	gift.open()
}
```

.col-right[
```go
// The other goroutine
`gift := <- channel`
gift.open()
```
]

<img src="content/images/gift4.jpg" alt="Gift 4" width="90%" style="margin-top: 0rem;">

---

# Every language lets you give

```go
func foo() {
	gift := Gift { .. }
	channel <- gift
	`gift.open()`
}
```

.col-right[
```go
// The other goroutine
`gift := <- channel`
gift.open()
```
]

<img src="content/images/gift5.jpg" alt="Gift 5" width="90%" style="margin-top: 0rem;">

---

# Every language lets you give

```go
func foo() {
	gift := Gift { .. }
	channel <- gift
	`gift.open()`
}
```

.col-right[
```go
// The other goroutine
gift := <- channel
`gift.open()` // data race
```
]

<img src="content/images/gift5.jpg" alt="Gift 5" width="90%" style="margin-top: 0rem;">

---

# What went wrong?

Two ingredients:

- Mutation
- Sharing

--

Rust's solution:

- Ownership and borrowing
- Support sharing and mutation
  - but **not at the same time**

---

# Rust lets you take away

```rust
fn foo() {
  let gift = Gift::new();
  channel.send(gift);
  gift.open();
}
```

.col-right[
````rust
impl<T> Channel<T> {
  fn send(&mut self, data: T) {
    // ...
  }
}
```
]

<img src="content/images/gift1.jpg" alt="Gift 1" width="90%" style="margin-top: 0rem;">

---

# Rust lets you take away

```rust
fn foo() {
  `let gift = Gift::new();`
  channel.send(gift);
  gift.open();
}
```

.col-right[
````rust
impl<T> Channel<T> {
  fn send(&mut self, data: T) {
    // ...
  }
}
```
]

<img src="content/images/gift2.jpg" alt="Gift 2" width="90%" style="margin-top: 0rem;">

---

# Rust lets you take away

```rust
fn foo() {
  let gift = Gift::new();
  `channel.send(gift);`
  gift.open();
}
```

.col-right[
````rust
impl<T> Channel<T> {
  fn send(&mut self, data: T) {
    // ...
  }
}
```
]

<img src="content/images/gift3.jpg" alt="Gift 3" width="90%" style="margin-top: 0rem;">

---

# Rust lets you take away

```rust
fn foo() {
  let gift = Gift::new();
  `channel.send(gift);`
  gift.open();
}
```

.col-right[
````rust
impl<T> Channel<T> {
  fn send(&mut self, data: T) {
    // ...
  }
}
```
]

<img src="content/images/gift4.jpg" alt="Gift 4" width="90%" style="margin-top: 0rem;">

---

# Rust lets you take away

```rust
fn foo() {
  let gift = Gift::new();
  `channel.send(gift);`
  gift.open();
}
```

.col-right[
````rust
impl<T> Channel<T> {
  fn send(&mut self, `data: T`) {
    // ...
  }
}
```
]

<img src="content/images/gift6.jpg" alt="Gift 6" width="90%" style="margin-top: 0rem;">

---

# Rust lets you take away

```rust
fn foo() {
  let gift = Gift::new();
  channel.send(gift);
  `gift.open();`
}
```

.col-right[
````rust
impl<T> Channel<T> {
  fn send(&mut self, `data: T`) {
    // ...
  }
}
```
]

<img src="content/images/gift6.jpg" alt="Gift 6" width="90%" style="margin-top: 0rem;">

---

# Rust lets you take away

```rust
fn foo() {
  let gift = Gift::new();
  channel.send(gift);
  `gift.open();`
}
```

.col-right[
````rust
impl<T> Channel<T> {
  fn send(&mut self, `data: T`) {
    // ...
  }
}
```
]

```
error[E0382]: use of moved value: 'gift'
  --> src/main.rs:13:4
     |
  12 |    channel.send(gift)
     |                 ---- `value moved here`
  13 |    gift.open();
     |    ^^^^ `value used here after move`
```

---

# Memory safety: a strict compiler

- It can take some time until your program compiles
- Lifetimes can be complicated
    - “error: `x` does not live long enough”


However:
- “If it compiles, it usually works”
- Far less debugging
    - No data races!
- Refactoring is safe and painless

???

- Prevents bugs, double free, dangling pointers, null references and buffer overflows.
- Instead of relying on a garbage collector, it uses an ownership system with strict compile-time checks.
- The compiler enforces rules to prevent data races at compile time.
- Makes multithreaded programming much safer and easier.

---

<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto" style="position: absolute; right: 0rem; margin-top: -2rem;">

# Why people love Rust?

- Performance
- Memory safety without GC
- **Fearless concurrency**

---

# Fearless concurrency

```rust
use std::thread;

fn main() {
    let mut s = String::from("Hello");
    
    thread::spawn(move || {
        s.push_str(" World!");
    });

    println!("{s}");
}
```

---

# Fearless concurrency

```rust
use std::thread;

fn main() {
    let mut `s` = String::from("Hello");
    
    thread::spawn(move || {
        `s`.push_str(" World!");
    });

    println!("{`s`}");
}
```

---

# Fearless concurrency

```code
error[E0382]: borrow of moved value: s
   |
4  |     let mut s = String::from("Hello");
   |         ----- move occurs because s has type String, which does not implement the Copy trait
5  |     
6  |     thread::spawn(move || {
   |                   ------- value moved into closure here
7  |         s.push_str(" World!");
   |         - variable moved due to use in closure
...
10 |     println!("{s}");
   |                ^ value borrowed here after move
   |

For more information about this error, try rustc --explain E0382.
```

---

<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto" style="position: absolute; right: 0rem; margin-top: -2rem;">

# Why people love Rust?

- Performance
- Memory safety without GC
- Fearless concurrency
- **Powerful type system**
  - **High-level code, low-level performance**

---

# Ownership

```rust
fn foo() {
  let `gift` = Gift::new();
  channel.send(`gift`);
  gift.open();
}
```

.col-right[
````rust
impl<T> Channel<T> {
  fn send(&mut self, `data`: T) {
    // ...
  }
}
```
]

---

# Ownership

```rust
fn foo() {
  let gift = Gift::new();
  channel.send(gift);
  `gift`.open();
}
```

.col-right[
````rust
impl<T> Channel<T> {
  fn send(&mut self, data: T) {
    // ...
  }
}
```
]

---

# Borrowing

```rust
fn foo() {
  let gift = Gift::new();
  channel.send(gift);
  gift.open();
}
```

.col-right[
````rust
impl<T> Channel<T> {
  fn send(`&mut self`, data: T) {
    // ...
  }
}
```
]

---

# High-level code

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

Algebraic data types (enums), Pattern matching & Hygienic macros

---

# High-level code

```rust
enum Event {
    Load,
    KeyPress(char),
    Click { x: i64, y: i64 }
}

fn print_event(event: Event) {
    match event {
        Event::Load => println!("Loaded"),
        Event::KeyPress(`c`) => println!("Key {} pressed", `c`),
        Event::Click {x, y} => println!("Clicked at x={}, y={}", x, y),
    }
}
```

Algebraic data types (enums), Pattern matching & Hygienic macros

---

# High-level code

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
        Event::Click {`x`, `y`} => println!("Clicked at x={}, y={}", `x`, `y`),
    }
}
```

Algebraic data types (enums), Pattern matching & Hygienic macros

---

# No null pointers

```rust
fn print_first(v: Vec<String>) {
  let s = v.first();
  println!("{}", s.to_uppercase());
}
```

--

```code
error[E0599]: no method named `to_uppercase` found for enum `Option`
       in the current scope
   --> src/main.rs:3:20
    |
3   |   println!("{}", s.to_uppercase());
    |                    ^^^^^^^^^^^^ method not found in `Option<&String>`
    |
note: the method `to_uppercase` exists on the type `&String`

For more information about this error, try `rustc --explain E0599`.
```

---

# No null pointers

```rust
enum Option<T> {
  Some(T),
  None,
}
```

Generics

---

# No null pointers

```rust
fn print_first(v: Vec<String>) {
  match v.first() {
    Some(s) => println!("{}", s.to_uppercase()),
    None => println!("Not found"),
  }
}
```

---

# No null pointers

```rust
fn print_first(v: Vec<String>) {
  match v.first() {
    Some(`s`) => println!("{}", `s`.to_uppercase()),
    None => println!("Not found"),
  }
}
```

---

# High-level code

```rust
fn load_images(paths: &[PathBuf]) -> Vec<Image> {
    paths.iter()
         .map(|path| Image::load(path))
         .collect()
}
```

Iterators, Traits, Generics & Closures

---

# Powerful type system: mutexes

```rust
// mutex owns data
let mutex = Mutex::new(data);

// compilation error: data was moved
data.push(4);

let mut d = mutex.lock().unwrap();
d.push(5);
// released at end of scope
```

⇒ Rust ensures that Mutex is locked before accessing data

???

- Impossible to access data behind a Mutex without locking
- Represent contracts in code instead of documentation

---
<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto" style="position: absolute; right: 0rem; margin-top: -2rem;">

# Why people love Rust?

- Performance
- Memory safety without GC
- Fearless concurrency
- Powerful type system
  - High-level code, low-level performance
- **Modern conveniences**
  - **Tooling**

---

<img src="content/images/cargo-logo.png" alt="Cargo logo" width="150rem" height="auto" style="position: absolute; right: 0rem; margin-top: -2rem;">

# Great tooling

- **rustup**: Use multiple Rust versions for different directories
- **cargo**: Automatically download, build, and link dependencies

.center[
<img src="content/images/cratesio.png" alt="Crates.io screenshot" width="500rem">
]

???

- rustup: Rust installer
- cargo: package manager and build tool.
- Strong compiler messages that are clear and educational.

---

<img src="content/images/cargo-logo.png" alt="Cargo logo" width="150rem" height="auto" style="position: absolute; right: 0rem; margin-top: -2rem;">

# Great tooling

- **rustup**: Use multiple Rust versions for different directories
- **cargo**: Automatically download, build, and link dependencies
- **rustfmt**: Format Rust code according to style guidelines
- **clippy**: Additional warnings for dangerous or unidiomatic code

--
- **Rust Playground**: Run and share code snippets in your browser

![Rust Playground screenshot](content/images/playground.png)

???

- rustfmt: code formatter.
- clippy: A collection of lints to catch common mistakes and improve your Rust code.

---

<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto" style="position: absolute; right: 0rem; margin-top: -2rem;">

# Why people love Rust?

- Performance
- Memory safety without GC
- Fearless concurrency
- Powerful type system
  - High-level code, low-level performance
- Modern conveniences
  - Tooling
- **Community**

---

# Community

.center[
<img src="content/images/community.jpg" alt="Rust community" width="650rem">
]

???

Open, friendly, welcoming, inspiring, craftmanship, learn

---

# To sum up

- **Rust is a high perfomant and safe systems programming language**

---

# To sum up

- Rust is a high perfomant and safe systems programming language
- **"Everyone" is heavily investing in it (Linux Kernel, Google, Amazon, Microsoft, Meta (Facebook), Mozilla, etc)**

---

# To sum up

- Rust is a high perfomant and safe systems programming language
- "Everyone" is heavily investing in it (Linux Kernel, Google, Amazon, Microsoft, Meta (Facebook), Mozilla, etc)
- **People love Rust**
  - **Performance**
  - **Memory safety without GC**
  - **Fearless concurrency**
  - **Powerful type system**
  - **Modern conveniences**
  - **Community**

---

# To sum up

- Rust is a high perfomant and safe systems programming language
- "Everyone" is heavily investing in it (Linux Kernel, Google, Amazon, Microsoft, Meta (Facebook), Mozilla, etc)
- People love Rust
  - Performance
  - Memory safety without GC
  - Fearless concurrency
  - Powerful type system
  - Modern conveniences
  - Community
- **Give it a try?**

---

class: center
name: title
count: false

<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto">

# Thanks

.grey[Github/Everywhere: spastorino]<br/>
.grey[Email: spastorino@gmail.com]
