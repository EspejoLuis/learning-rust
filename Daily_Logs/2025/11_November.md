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

## ☀️ 10th November - Monday

- 🎥 [Visualizing memory layout of Rust's data types](https://www.youtube.com/watch?v=7_o-YRxf_cc&t=1661s): Long video but interesting. It explain the allocation of each variable type. To watch again!

### Chapter 3 - Commong Programming Concepts - Data Types

- Data types can be:
  - **Scalar**
    - **Integer**: signed(i)/unsigned(u).

      | Length                | Signed | Unsigned |
      |-----------------------|---------|-----------|
      | 8-bit                 | i8      | u8        |
      | 16-bit                | i16     | u16       |
      | 32-bit                | i32     | u32       |
      | 64-bit                | i64     | u64       |
      | 128-bit               | i128    | u128      |
      | Architecture dependent | isize   | usize     |

      - Signed -> from $0$ to $2^{n} − 1$
      - Unsigned -> from $−2^{n − 1}$ to $2^{n − 1} − 1$
      - isize/usize can be used when indexing some sort of collection.
      - Default is i32.

        ```rust
        fn main() {
            let x = 2; // default i32
        }
        ```

      - *integer overflow*: for example, when using an u8 variable and and assigment of 256 is done. Maximum being 255 (from 0 to 255). What happens ?
        - Debug --> Programm will panic!
        - Release --> No panic but Rust will perform wrapping i.e. it will start from scratch. Basically, 256 will be 0, 257 will be 1 etc.

    - **Floating-point**:
      - Floating points are signed by default.
      - They can be f32 or f64.
      - f64 is the default.

      ```rust
      fn main() {
          let x = 2.0; // default f64
      }
      ```

    - **Booleans**:

    ```rust
        fn main() {
        let t = true;
        let f: bool = false; // with explicit type annotation
    }
    ```

    - **Characters**: `char` literals (with single quote) are different from string literal (with double quotes). Rust's `char` is four bytes and represents a *unicode* so more than just *ASCII*. It can be also emojis!

    ```rust
    fn main() {
    let c = 'z';
    let z: char = 'ℤ'; // with explicit type annotation
    let heart_eyed_cat = '😻';
    }
    ```

## ☀️ 11th November - Tuesday

### Chapter 3 - Commong Programming Concepts - Data Types - Part II

- **Compound**: There are two primitive compound types:
  - **Tuple**: fixed collection of possible different type variables.

    ```rust
    fn main() {
    let tup = (500, 6.4, 1);
    // Alternatively let tup: (i32, f64, u8) = (500, 6.4, 1);

    let (x, y, z) = tup; // --> Destructuring !

    println!("The value of y is: {y}");
    }
    ```

    Tuples can be accessed:

    ```rust
    fn main() {
    let x: (i32, f64, u8) = (1, 2.4, 4);

    let five_hundred = x.0
    let six_point_four = x.1;
    let one = x.2;
    }
    ```

    - Tuples without any value are called **unit**:
            - Its *value* and *type* are both `()`.
            - Expression that do not return anything, implicitly return the unit value.
            - `()` is an actual type. In C++ `void` is not a real type, it cannot be assigned/stored.

        ```rust
        let a: () = (); // It works!
        ```

    - Tuples are *not immutable* like in python!

      ```rust
      fn main() {
      let mut x: (i32, i32) = (1, 2);
        x.0 = 0;
        x.1 += 5;
      }
      ```

    - Stored in the stack.
    - Not an iterable.

  - **Array**: fixed collection of same type variables.

    ```rust
    let a: [i32; 5] = [1, 2, 3, 4, 5];
    ```

    - When arrays can be used ?
      - To allocate data on the stack.
      - To ensure there are only a fixed number of elements.
      - To iterate.

    - vs Vector: vectors are allowed to grow. Vectors live in the heap. More in later chapters.
    - You can declare same value automatically. Below you have an array of five elements. All are thress.

    ```rust
    let a = [3; 5]; // [3,3,3,3,3]
    ```

    - How to access them ?

    ```rust
    fn main() {
    let a = [1, 2, 3, 4, 5];

    let first = a[0];
    let second = a[1];
    }
    ```

    C++ does not perform runtime bounds checking on arrays or most containers. On the other hand, Rust performs runtime bounds checking on arrays. This avoids invalid memory to be accessed. Basically, Rust immediately exits (and panics).

## ☀️ 12th November - Wednesday

### Chapter 3 - Commong Programming Concepts - Functions

- **Parameters**:
  - Parameters vs Arguments:

    - Variables in a function definition are called *parameters*. These are special values defind in function's signature.

    - Actual values are defined as *arguments*.

  - If there are parameters in the definition of a function, those parameters must have a `types`. It's better for the compiler!.

- **Statement and Expression**:
  - What are functions ? Just a series of different statements with an optional expression at the end.

  - What's the difference ?
    - *Statements*: instructions that perform some action but do not return anything.
    - *Expression*: evaluate to a resultant value.

  - Function definition is a statment, `let y = 6` is a stement as well.

  ```rust
  fn main() {
    let y = 6;
  }
  ```

  - Because `let y = 6` is a statement, it cannot be assigned to another `let`. In C++ you can do `x=y=6`.
  - `6` is `let y = 6;` is an expression.

  - Calling a function is an expression.
  - A new scope in curly brackets `{}` is an expression.

  ```rust
  fn main() {
    let y = {.    // Expression
        let x = 3;// Expression
        x + 1     // Expression no ; !
    };
    println!("The value of y is: {y}");
  }
  ```

  - Expression do not include `;`. If a semicolon `;` is added then the expression becomes a statement. And do not return anything!.

## ☀️ 14th November - Wednesday

### Chapter 3 - Commong Programming Concepts - Functions - Part II

- **Functions with Return Values**

  - No name for return values but only type in functions (`->`).
  - Most functions return the last expression implicilty. If there is no expression then the function returns the unit type `()`. In the code below the function `plus_one()` has a return type of `i32` but no expression in the its scope so the return value and type is `()` which of course cause Rust to panic.

    ```rust
    fn main() {
      let x = plus_one(5);
      println!("The value of x is: {x}");
    }

    fn plus_one(x: i32) -> i32 {
        x + 1;
    }
    ```

- **Comments**

  - Simply use `//` and `/* */`

- **Control Flow**

  - **If**
    - In C++, `if` conditions are by default checked against zero. In Rust, this is not true. `if` expects an explicity boolean condition.

    - `if` in a `let` statement: `if` is an *expression* so we can use in the rigth side of an a `let` statement.

      ```rust
      fn main() {
        let condition = true;
        let number = if condition { 5 } else { 6 };

        println!("The value of number is: {number}");
      } 
      ```

    - Branches of `if` conditions must be of same type!
    - Blocks of code evaluates to the last expression in them, and numbers alone are still expression.
    - The following code will give an error. Rust needs to know `number` type at compile time. Uniquely.

      ```rust
      fn main() {
        let condition = true;

        let number = if condition { 5 } else { "six" };

        println!("The value of number is: {number}");
      }
      ```

  - **Loop**
    - `loop`: you can `break` it and if you want a result put it after the `break`.

        ```rust
        fn main() {
        let mut counter = 0;

        let result = loop {
            counter += 1;

            if counter == 10 {
                break counter * 2;
            }
        };

        println!("The result is {result}");
        }
        ```

      - `break` exits loop, `return` exits function.
      - The semicolon `;` after `break counter * 2` is optional.
      - Code after (as in the next lines after) `break` or `return` is never executed. `break;` and `return;` are expression and treated as having value unit `()`.

      - Label in multiple `loops`.

        ```rust
        fn main() {
        let mut count = 0;
        'counting_up: loop {
            println!("count = {count}");
            let mut remaining = 10;

            loop {
                println!("remaining = {remaining}");
                if remaining == 9 {
                    break; // This break the inner loop only
                }
                if count == 2 {
                    break 'counting_up; //This break the outer loop
                }
                remaining -= 1;
            }

            count += 1;
        }
        println!("End count = {count}");
        }
        ```

    - Conditional loops: `while`.

      ```rust
      fn main() {
      let mut number = 3;

      while number != 0 {
          println!("{number}!");

          number -= 1;
      }

      println!("LIFTOFF!!!");
      }
      ```

      While loop could be also used to loop through an array. However, it is not really that safe. Code could panic if the index is wrong for example if the array size changes to be four.

      ```rust
      fn main() {
      let a = [10, 20, 30, 40, 50];
      let mut index = 0;

      while index < 5 {
          println!("the value is: {}", a[index]);
          index += 1;
      }

      }
      ```

    - `for` loop: insted of previous loop, better to use `for` loop.

      ```rust
      fn main() {
      let a = [10, 20, 30, 40, 50];

      for element in a {
        println!("the value is: {element}");
        }
      }
      ```

      Even for cases where there is a condition, most people will use `for` rather than `while`:

      ```rust
      fn main() {
       for number in (1..4).rev() {
        println!("{number}!");
        }
        println!("LIFTOFF!!!");
      }
      ```

## ☀️ 16th November - Sunday

About ownerships/borrowing:

- 🎥 Video: [Learning Rust: Memory, Ownership and Borrowing](https://www.youtube.com/watch?v=8M0QfLUDaaA&t=12s)

- 🎥 Video: [04 Ownership & Borrowing | Rust Tutorials](https://www.youtube.com/watch?v=q2UnbA2dkc8)

## ☀️ 17th November - Monday

### Chapter 4 - Understanding Ownetship - What is ownership ?

- What are Rust's goals:
  1. Ensuring that the program does not have any undefined behaviour. i.e. ensuring safety! This can be particularly important when it comes to low level programming languages that have direct access to memory.
  2. Prevent undefined behavoiour at compile-time instead of run-time.

- With this goals in mind, `ownership` is a discipline for safely using memory!

- *Variable live in the stack*

  - Variables live in frames. What is a frame ? it is a mapping from variables to values within a single scope, such as a function.

  ![alt text](<Screenshot 2025-11-17 at 20.15.11.png>)

  - In this picture there are many frames:
    - Frame for `main`, at L1/L2/L3.
    - Frame for `plus_one` at L2.

  - All frames are then grouped into a stack. They are deallocating follownig LIFO pattern.
  - When a functions returns, the function's frame is deallocated.
  - Deallocation/Freeing/Dropping are synonimous in the book.

  - When variables defined enitrely in the stack are assigned, variables's value is copied by default in the stack. Example below:

  ![alt text](<Screenshot 2025-11-17 at 20.24.58.png>)

  - New variable `b` can be modified without altering the original variable `a` because they are copies.

  - Variables can also be defined in the heap ("free store") where data can live indefintely. In the heap, variables do not follow any stack frame rule.
  
  - `Box` can be used to define variables in the heap. Allocating memory in the heap is a way to make a pointer.

  - A pointer contains the address of a variable, basically it describes the location in the memory. This memory can be heap memory.

  ![alt text](<Screenshot 2025-11-17 at 20.31.47.png>)

  - When assigning `let b = a`, pointer from `a` is copied to `b`. Only the pointer is copied, not the pointed-at value.

  - `a` is greyed out because it has been moved.

  - Only one variable can own the pointer at any time.

  - In the picture, the pointer is in the stack. Pointer to the heap. However, we can also have pointers in the heap to the stack.

  - Frames in the stack are linked to specific funtioncs and deallocated as soon as the function returns. In the heap, data can leave indefinitely --> Both in the stack and in the heap, data can be copyable and mutable.

  - Video 🎥 [Rust String vs str slices](https://www.youtube.com/watch?v=ClPrjjHmo2Y)

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

## 🎥 Videos

- 🎥 [Visualizing memory layout of Rust's data types](https://www.youtube.com/watch?v=7_o-YRxf_cc&t=1661s). Long video but interesting. It explain the allocation of each variable type. To watch again!
