class: center
name: title
count: false

<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto">

# Why Rust?

.grey[Santiago Pastorino]

.grey[.smaller[WyeWorks, Rustc, Rust Latam, Rails core alumni]]

---

<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto" style="position: absolute; right: 0rem; margin-top: -2rem;">

# What is Rust?

- "New" & safe systems programming language
  - Developed by Mozilla research, v1.0 released in 2015
- Multiparadigm
  - Imperative, structured, functional, concurrent, generic, compiled
- Static strong typing
  - Inference
- Emphasizing control, safety, and speed
- Free and open-source software, MIT License or Apache License 2.0

---

# Who is using Rust?

- **Mozilla** - Stylo, WebRender.
- **Google** - Fuchsia operating system.
- **Facebook** - Libra.
- **Amazon** - Firecracker.
- **Microsoft** - Azure IoT work.
- **Dropbox** - Storage system.

You can see even more familiar names like **Twitter**, **npm**, **Red Hat**, **Reddit**, **Samsung**, **Cloudflare**, **Gnome**, **Chef**, **Canonical**, **Coursera**, **Tor** and many more.

Being used also for **WebAssembly**, **Web APIs**, **Blockchain**, **Networking**, **Embedded**, **Games**. **Native Extensions**, etc.

---

<img src="content/images/technology-radar.png" alt="Thoughtworks Radar">

Lot of interest in Rust, some of our clients are already using it.

---

# People love Rust (2016)

<img src="content/images/most-loved-2016.png" alt="Stackoverflow Survey">

---

# People love Rust (2017)

<img src="content/images/most-loved-2017.png" alt="Stackoverflow Survey">

---

# People love Rust (2018)

<img src="content/images/most-loved-2018.png" alt="Stackoverflow Survey">

---

# People love Rust (2019)

<img src="content/images/most-loved-2019.png" alt="Stackoverflow Survey">

---

<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto" style="position: absolute; right: 0rem; margin-top: -2rem;">

# Why people love Rust?

- **Performance**
  - **Zero-cost abstractions**

---

# Performance

<img src="content/images/performance.png" alt="Performance Rust/C/C++">

---

# Qualities Rust shares with C(++)

- **Zero-cost abstractions:**
  - inline memory layout
  - static dispatch
  - no garbage collector or other runtime
- Anywhere you use C(++), you can use Rust:
  - Want to write a plugin for Python or Ruby? You can do it in Rust.
  - Want to write a **kernel**? You can do it in Rust.

---

# Why not just use C(++) then?

---

<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto" style="position: absolute; right: 0rem; margin-top: -2rem;">

# Why people love Rust?

- Performance
  - Zero-cost abstractions
- **Memory safety without GC**
  - **Concurrency without dataraces**

---

# Memory safety

<img alt="Linux CVEs in 2018" src="content/images/Linux CVEs in 2018.svg" style="margin-top: 0rem; margin-bottom: -2rem;">

<img src="content/images/Tux.svg" alt="Linux logo" width="120rem" height="auto" style="display:block; position: absolute; top: 1rem; right: 3rem;">

.grey[.smaller[Source: https://www.cvedetails.com/vulnerability-list/vendor_id-33/product_id-47/year-2018/Linux-Linux-Kernel.html]]

---

# Memory safety

<img alt="Microsoft Memory Safety" src="content/images/microsoft-memory-safety-trends.png" style="margin-top: 0rem; margin-bottom: -2rem;">

.grey[.smaller[Source: https://www.zdnet.com/article/microsoft-70-percent-of-all-security-bugs-are-memory-safety-issues/]]

---

# Parallel CSS Styling

<img src="content/images/bug-631527.png" alt="Firefox 8 years bug fixed by Stylo">

Reported 8 years ago

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

???

Guaranteed by Rust's ownership system at compile time

---

# Every language lets you give

```go
func foo() {
	gift := Gift { .. }
	channel <- gift
	gift.open()
}
```

<img src="content/images/gift1.jpg" alt="Gift 1">

---

# Every language lets you give

```go
func foo() {
	`gift := Gift { .. }`
	channel <- gift
	gift.open()
}
```

<img src="content/images/gift2.jpg" alt="Gift 2">

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

<img src="content/images/gift3.jpg" alt="Gift 3">

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

<img src="content/images/gift4.jpg" alt="Gift 4">

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

<img src="content/images/gift5.jpg" alt="Gift 5">

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

<img src="content/images/gift5.jpg" alt="Gift 5">

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

<img src="content/images/gift1.jpg" alt="Gift 1">

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

<img src="content/images/gift2.jpg" alt="Gift 2">

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

<img src="content/images/gift3.jpg" alt="Gift 3">

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

<img src="content/images/gift4.jpg" alt="Gift 4">

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

<img src="content/images/gift6.jpg" alt="Gift 6">

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

<img src="content/images/gift6.jpg" alt="Gift 6">

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

---

<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto" style="position: absolute; right: 0rem; margin-top: -2rem;">

# Why people love Rust?

- Performance
  - Zero-cost abstractions
- Memory safety without GC
  - Concurrency without dataraces
- **Powerful type system**
  - **High-level code, low-level performance**

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
enum Option<T> {
  Some(T),
  None,
}
```

Generics

---

# No null pointers

```rust
enum Option<T> {
* Some(T),
  None,
}
```

Generics

---

# No null pointers

```rust
enum Option<T> {
  Some(T),
* None,
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
  - Zero-cost abstractions
- Memory safety without GC
  - Concurrency without dataraces
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

---

<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto" style="position: absolute; right: 0rem; margin-top: -2rem;">

# Why people love Rust?

- Performance
  - Zero-cost abstractions
- Memory safety without GC
  - Concurrency without dataraces
- Powerful type system
  - High-level code, low-level performance
- Modern conveniences
  - Tooling
- **Community**

---

# Community

.center[
<img src="content/images/community.jpg" alt="Rust community" width="650rem">

.smaller[Open, friendly, welcoming, inspiring, craftmanship, learn]
]

---

# To sum up

- **Rust is a high perfomant and safe systems programming language**

---

# To sum up

- Rust is a high perfomant and safe systems programming language
- **Used by a lot of big names already (Mozilla, Google, Facebook, Amazon, Microsoft, Twitter, Dropbox, etc)**

---

# To sum up

- Rust is a high perfomant and safe systems programming language
- Used by a lot of big names already (Mozilla, Google, Facebook, Amazon, Microsoft, Twitter, Dropbox, etc)
- **People love Rust**
  - **Performance**
  - **Memory safety without GC**
  - **Powerful type system**
  - **Modern conveniences**
  - **Community**

---

# To sum up

- Rust is a high perfomant and safe systems programming language
- Used by a lot of big names already (Mozilla, Google, Facebook, Amazon, Microsoft, Twitter, Dropbox, etc)
- People love Rust
  - Performance
  - Memory safety without GC
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

.grey[Twitter/Github: spastorino]<br/>
.grey[Email: spastorino@gmail.com]
