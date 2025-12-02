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

