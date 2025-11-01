# November 2025

## ☀️ 1st November - Saturday

### Chapter 2 - Programming a Guessing Game

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

- `crate` is a collection of Rust source code files.

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

## Start From

[Left here](https://rust-book.cs.brown.edu/ch02-00-guessing-game-tutorial.html#:~:text=Rust%20Programming%20Language-,Programming%20a%20Guessing%20Game,-Let%E2%80%99s%20jump%20intohttps://rust-book.cs.brown.edu/ch01-03-hello-cargo.html#:~:text=Building%20and%20Running%20a%20Cargo%20Project)

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
