# December 2025

## ☀️ 2nd December - Tuesday

### Chapter 4 - Understanding Ownership - References and Borrowing

- One way to use variable. Not really that efficient though.

![alt text](<Screenshot 2025-12-02 at 21.43.35.png>)

- Better alternative is using `reference` (`&`):
  - Using references perfectly respect the **Box deallocation principle**. `m1` owns heap string "Hello" but `g1` doesn't, so when frame `greet()` ends, there is no deallocation of the heap memory. Rust did not deallocate the string on behalf of `g1`.
  - Reference are not owning pointers !

![alt text](<Screenshot 2025-12-02 at 21.47.50.png>)

- Deferencing a pointer: in previous cases no deference (`*`) has been shown, however Rust use them under the hood.

![alt text](<Screenshot 2025-12-02 at 21.55.25.png>)

- Rust does implicit deferencing. Some examples:

![alt text](<Screenshot 2025-12-02 at 22.00.47.png>)

- Interesting exercise:

![alt text](<Screenshot 2025-12-02 at 22.03.04.png>)

## ☀️ 3nd December - Wednesday

### Rust avoids simultaneous Aliasing and Mutation

- Aliasing means being able to access the same data using different variables. Having the option to use aliases and mutatation however can be a problem.

- There can be three different type of issues:
  - _Mutation of the aliased variable_: what happens to the code for the other variable ?
  - _Deallocation of the alliased variable_: the other variable then what does it do ?
  - _Mutatating the aliased variable at same time_: **data race** with non deterministic behaviour for the other variable.

- Example of macro `vec![]`. Difference from array is that `vec` is not fixed at compile time.

![alt text](<Screenshot 2025-12-03 at 20.38.58.png>)

- Important point is that a vector has length and capacity. And that the vector created above is at capacity, so if we add another element with push, new memory has to be creataed. This new memory will have to contained the old `v` and the new element. So the process:
  - Create new heap empty.
  - Copy old heap into new heap.
  - Deallocate old heap.
  
![alt text](<Screenshot 2025-12-03 at 20.57.47.png>)

- Rust book says that new heap could be "potentially" different from the old one.

- We need something that checks references and keeps everything safe. Otherwise we could have something like:

![alt text](<Screenshot 2025-12-03 at 21.04.16.png>)

- We have an undefined behaviour because the vector `v` is both aliased (`num`) and mutated with `v.push(4)`. To avoid this there is a principle:

Pointer Safety Principle: data should never be aliased and mutated at the same time. Either aliased or mutated.

- How does Rust enforce the pointer safety principle ?
  - **Owned Pointers** (like Boxes): Rust disallow aliases!
    - Assigning a box will move ownership, so the previous variable can't mutate.
    - Owned data can only be accessed through the owner and no aliases.
  - **Not Owned Pointers** (i.e. references):
    - Need different rules! By design, references are meant to create aliases (temporarily) --> Solution ? Borrow Checker.

### References changes permission on places

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

