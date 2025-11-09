# November 2025

## ☀️ 1st November - Saturday

### Chapter 2 - Programming a Guessing Game - Part I

- The Chapter gives a first overview, nothing major. It opens many doors but all will be explained in next chapters.

- Variables are immutable by default, so to declare a mutable variable, need to be specific:

  ```rust
  let mut guess = String::new()
  ```

- `read_line` returns a `result`. `result` is an enumeration, i.e. a type that can be in multiple possible states. Each state is called `variant`.

  ```rust
  io::stdin().read_line(&mut guess).expect("Failed to read line");
  ```

  In this case, `result` has two possible `variants`:
  - `Ok` -> operation succeeds and result contains the result of the operation.
  - `Err` -> operation fails and it contains all info about the failure.

- `crate` *is a collection of Rust source code files.*

- Process when we add a dependency in `[dependencies]`:
  - 0️⃣ Terminal: `cargo build` (or any `cargo` command).
  - 1️⃣ Checks the local cache (inside ~/.cargo/registry) to see if it already has that crate version.
  - 2️⃣ If not found, it contacts crates.io (the central registry) and fetches metadata (like versions and dependency trees).
  - 3️⃣ It then downloads all needed crates that aren’t already cached.
  - 4️⃣ It compiles all dependencies first, and then your project.

- The first time `cargo build` is run, all the dependencies are downloaded and compiled:

  ```rust
    Updating crates.io index
    Locking 15 packages to latest Rust 1.85.0 compatible versions
      Adding rand v0.8.5 (available: v0.9.0)
  Compiling proc-macro2 v1.0.93
  Compiling unicode-ident v1.0.17
  Compiling libc v0.2.170
  Compiling cfg-if v1.0.0
  Compiling byteorder v1.5.0
  Compiling getrandom v0.2.15
  Compiling rand_core v0.6.4
  Compiling quote v1.0.38
  Compiling syn v2.0.98
  Compiling zerocopy-derive v0.7.35
  Compiling zerocopy v0.7.35
  Compiling ppv-lite86 v0.2.20
  Compiling rand_chacha v0.3.1
  Compiling rand v0.8.5
  Compiling guessing_game v0.1.0 (file:///projects/guessing_game)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 2.48s
  ```

  If `cargo build` is typed again, and no changed has happened:
  
  ```rust
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.08s
  ```

  If a change is made in `main.rs` and then `cargo build`

  ```rust
   Compiling guessing_game v0.1.0 (/Users/apple/github_repos/learning-rust/projects/guessing_game)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.92s
  ```

## ☀️ 8th November - Saturday

### Chapter 2 - Programming a Guessing Game - Part II

- `cargo update` will update dependencies, up to next version. For example, if the version in the `Cargo.toml` is 0.8.5 then using `cargo update` will update all the version (if any) till but not including 0.9.

- When you declare variables at the beginning of the code, they could be modules, traits, struct etc. For example:

  ```rust
  use rand::Rng;
  use std::io;
  use std::cmp::Ordering;
  ```

  If it's in PascalCase then it could be a `trait`, `struct` or `Enum`. Lowercase is a `module`. `Rng` is a trait.

  Ordering is a enum whose variants are:
  - `Greater`
  - `Less`
  - `Equal`

- Rust defaults to `i32`  

- Very important command is `cargo doc --open` which builds the documentation of all the dependencies locally and open it in the browser. Cool!

- Rust allows users to do *shadowing*. Shadowing means that a variable name can be reused instead of creating a new name.

- Moving from an `expect` to a `match` makes possible to move from crashing to handling error. Examples below:
  
  ```rust
  let guess: u32 = guess.trim().parse().expect("Please type a number!");
  ```

  ```rust
  let guess: u32 = match guess.trim().parse() {
          Ok(num) => num,
          Err(_) => continue,
      };
  ```

## ☀️ 9th November - Sunday

### Chapter 3 - Commong Programming Concepts - Variables and Mutability

#### Intro

- By default all variables are immutable. The following code will not compile, i.e. compile error will appear, because it is assigning twice to `x` which is declared as immutable.

  ```rust
  fn main() {
      let x = 5;
      println!("The value of x is: {x}");
      x = 6;
      println!("The value of x is: {x}");
  }
  ```

- To compile,`x` needs to be declared as `mut`
  
  ```rust
  fn main() {
      let mut x = 5;
      println!("The value of x is: {x}");
      x = 6;
      println!("The value of x is: {x}");
  }
  ```

#### Constants

- Constants vs Immutable variables:
  - *Similarity*: `const` is a variable that is always immutable. `mut` can't be used.
  - *Difference*:
    - `const` can be declared in global scope. Other variables only in functions.
    - `const` has to be set equal to a constant expression i.e. expression defined at compile time not runtime!
  - example:
  
  ```rust
  const ANY_NAME: u32 = 60 * 60 * 3;
  ```

#### Shadowing

- What is it ? When a new variable is defined using same name of another variable.
- How to do it ? Using same variable name and `let`.

  ```rust
  fn main() {
      let x = 5;
      let x = x + 1;
      {
          let x = x * 2;
          println!("The value of x in the inner scope is: {x}");
      }
      println!("The value of x is: {x}");
  }
  ```

  In this case, the first variable `x=5` is shadowed by the second one `x=x+1`. From when it is shadowed, the variable stays the same untill it's shadowed again or the scope ends. For example, after `x=x+1`, there is another shadowing in a specific scope and within that scope `x` is shadowed `x=x*2`. Output will be:

  ```bash
  The value of x in the inner scope is: 12
  The value of x is: 6
  ```

- **Vs Mutable Variable** :

  Using *mutable variables*, same `x` changes over time, `x` has same memory location and type but value stored changes:

  ```rust
  let mut x = 5;
  x = x + 1;
  ```
  
  *Shadowing* does not mutate the same variable, each time `let` is used, a new variable is created. The new variable has its own memory and type:

  ```rust
  let x = 5;
  let x = x + 1;
  ```

  We already saw this case above, but just to reiterate the concepts, the following code will not compile

  ```rust
  let x = 5;
  x = x + 1;
  ```

  Shadowing creates a new variable whose type can be different from previous variable. This is another difference that sometimes might help. Instead of creating a variable with `spaces_str` and one `space_len`, the same variable can be used.

  ```rust
  let spaces = "   ";
  let spaces = spaces.len();
  ```

  This will not be possible, even with `mut`. Following code will not compile

  ```rust
  let mut spaces = "   ";
  spaces = spaces.len();
  ```

  Summary:
  - Shadowing creates a new variable with its own **memory** and **type**.

### Rustlings

- Done `01_Variables` exercises from 1 to 6.


## Start From

[Left here](https://rust-book.cs.brown.edu/ch03-00-common-programming-concepts.html)

## 📚 To Do

- [X] Read book - Fast.
- [ ] Read Book Second Time.
- [ ] Check Videos!
- [ ] Rustling.
- [ ] Rust by example.
- [ ] Acquascope for ownership concept/stack/heap.
- [ ] Check Comprehensive Rust
- [ ] Refresh topics:

  - [ ] Heap, stack and dynamic memory
  - [ ] Memory allocation and deallocation
  - [ ] Manual memory management vs garbage collector
  - [ ] Concurrency, parallelism and multithreading
  - [X] Compiled vs interpreted languages
