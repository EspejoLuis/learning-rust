# October 2025

## ☀️ 24th October - Friday

- Video: watching video from Jane Street -> [Rust for Everyone!](https://www.youtube.com/watch?v=R0dP-QR5wQo&t=542s):
  1. *Learning*:
        - Very interesting website to see visually the concept of `ownership` -> [Acqascope](https://cel.cs.brown.edu/aquascope/). In Aquascope you have ownership concept representation and also very useful representation of stack/heap variables.
        - There is also a link to a modified version of [The Rust Programming Language - Brown Version](https://rust-book.cs.brown.edu/). This version containes quizzes and more graphs to help with understanding of rust.
  2. *Trait Debugger*:
        - [Argus](https://github.com/cognitive-engineering-lab/argus). Can be useful I think, to try. IDE plugin.
  3. *A Program Slicer*:
        - [Flowistry](https://github.com/willcrichton/flowistry). IDE pluging that highlights part of the code that impacts/are impacted by the variable you are pointing at.

- Checking some website:
  - [getcracked.io](https://getcracked.io/questions). Seems good (also for Python/C++)
  - This guy is good!

## ☀️ 25th October - Saturday

- It's always good to start from what <u>not to do</u> (Taleb would be so proud!), found some videos:
  - 🎥 Video [5 things I wish I knew before learning Rust](https://www.youtube.com/watch?v=EYCBm0xAWow&list=PLrAjGqHG72ioGO2OZFQCnKloyDj7jFURl):
    - Some interesting points:
      - Topics to refresh:
        - Heap, stack and dynamic memory.
        - Memory allocation and deallocation.
        - Manual memory management vs garbage collector.
        - Concurrency, parallelism and multithreading.
        - Compiled vs interpreted languages.
      - Suggesting to have prior experience in C/C++. I think yeah it would definitely help but I dont think it's a blocker. He suggests that learning C/C++ could make understanding easier. So it could be useful to always think in terms of what Rust is doing differently from C/C++. Not going to spend too much time in learning C/C++ at the beginning.
      - Suggests some links:
        - [The Cherno](https://www.youtube.com/@TheCherno) in youtube for C/C++ fundamentals.
        - [The Rust Language Tutorial](https://www.youtube.com/watch?v=OX9HJsJUDxA&list=PLai5B987bZ9CoVR-QEIN9foz4QCJ0H2Y8&index=1). This can be quite useful. Basically he goes through each chapter of [The Rust Programming Language](https://doc.rust-lang.org/book/ch01-00-getting-started.html) book which is quite cool. It can be used wrap up *after* reading the book.
        - [Rust by Examples](https://doc.rust-lang.org/rust-by-example/index.html). Series of exercises.
        - Useful repo for practising: [Rustlings repo](https://rustlings.rust-lang.org/).
        - Another useful repo that contains articles, best practices, books, workshops: [Idiomatic](https://github.com/mre/idiomatic-rust?tab=readme-ov-file).
        - Recommended also youtube channel [Jon Gjengset](https://www.youtube.com/@jonhoo) for more advance stuff. Seems cool!
    - Overall good video telling you where to find information!

  - 🎥 Video [How NOT to learn Rust](https://www.youtube.com/watch?v=2uY5tpcs3Gs&list=PLrAjGqHG72ioGO2OZFQCnKloyDj7jFURl&index=6):
    - Not trying to learn everything at once. Learn enought that you can start practising. After some videos and books there has to be practice.

  - 🎥 Video [How to Learn Rust](https://www.youtube.com/watch?v=2hXNd6x9sZs&list=PLrAjGqHG72ioGO2OZFQCnKloyDj7jFURl&index=9):
    - Basically [Rustlings](https://rustlings.rust-lang.org/) follows the chapter in the [The Rust Programming Language](https://doc.rust-lang.org/book/ch01-00-getting-started.html). Also [Rust by Examples](https://doc.rust-lang.org/rust-by-example/index.html) is loosely linked to the content of the book. Video suggests to keep them all together.
    - He suggested what I was already thinking, read the book twice without doing any exercise, simply to go through it. The second time use the [The Rust Programming Language - Brown Version](https://rust-book.cs.brown.edu/).
    - It suggest to read Haskel for having a functional view on programming:
      - "Real World Haskell: Code You Can Believe in"
      - "Learn You a Haskell for Great Good!: A Beginner's Guide: A Beginner's Guide to Haskell". This seems very basic. Maybe good.

✏️ Summary:

- Read the book [The Rust Programming Language](https://rust-book.cs.brown.edu/) maybe one time, fast, view of all could be helpful.

- Review some topics/concepts.

- Install [Rustlings](https://rustlings.rust-lang.org/) --> Done.

## ☀️ 26th October - Sunday

- Starting reading [The Rust Programming Language](https://rust-book.cs.brown.edu/) very fast and mindmapping it as well (just main chapters). Reached chapter 13.

## ☀️ 27th October - Monday

- Fast read till chapter 20. Just two left.

## ☀️ 28th October - Tuesday

### Chapter 1 - Getting Started - Part 1

- Macros can be recognized because they have `!` at the end of the name. For example `println!`.

- To compile use `rustc main.rs`. This will create the executable `main`. Note: anyone can run the main. Theoretically that file can be given to someone who does not have Rust intalled `main` it will run anyway.

- To create a project with cargo (i.e. Rust's building system and package manager) type in terminal: `cargo new hello_cargo`. This will crate a folder named `hello_cargo` with `src` folder in it and `main.rs` in it. Moreover, it will create the *Cargo.toml* file.

- `cargo init` creates the *Cargo.toml*.

### Note

- **Compiled languages**: the program is translated entirely into machine code before it runs.
  1. Write source code
  2. A *compiler* translates it into a standalone executable (binary).
  3. When you run that binary, the CPU executes the machine instructions directly.

- **Interpreted languages**: the program is translated and executed line-by-line at runtime by another program called an interpreter.
  1. Write source code
  2. The *interpreter* reads the code and executes it directly, translating it as it goes.

- Python is an hybrid example: the source code is translate into .pyc (bytecode files) and then interpreted by the Python Virtual Machine.

## ☀️ 29th October - Wednesday

### Chapter 1 - Getting Started - Part 2

- After having created the hello_cargo folder, in terminal `cargo build` will create:
  - `target` folder. By default, building is considered for debug purposes, so a `debug` folder is created and within it, a the hello_cargo **executable** is created as well. To run it `./target/debug/hello_cargo`
  
  ```bash
  Apples-MacBook-Pro:hello_cargo apple$ cargo build
    Compiling hello_cargo v0.1.0 (/Users/apple/github_repos/learning-rust/projects/hello_cargo)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 1.02s
  ```

  - `Cargo.lock`: this file keeps track the *version* of all dependencies. Do not modify ever, cargo will always take care of that.

- `cargo run` compiles and run at the same time in one command.

  ```bash
  Apples-MacBook-Pro:hello_cargo apple$ cargo run
   Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.05s
   Running `target/debug/hello_cargo`
   Hello, world!
  ```

- `cargo check` checks if the code compiles but no executable is produced. Producing an executable might take time, so `cargo check` makes easier to understand if the code is still working without spending time in creating the executable.

- To build not in debug mode, `cargo build --release`. This will create an **executable** within `release` folder. The release build is optimized so it can take longer than the debug version to compile.

- Committed rustlings repo and did first exercise.

## ☀️ 31th October - Friday

- 🎥 Interesting video about how Rust it's differnt from C++/Java: [How rust forces you to respect memory](https://www.youtube.com/watch?v=mlf7QYhXkdc). Very simple, yet effective.
