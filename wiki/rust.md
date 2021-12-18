[#](#) Rust

## Traits
## Ownership and Borrowing
## Lifetime Annotations
## String vs str
* String is held in heap and can be mutable (good for large text and text mutation)
* &str (aka string literal) is immutable and can be stack, heap, or embedded (good for speed)

```
let ex_str: &str = "Hello";
let ex_string: String = String::from("Hello");
```

Translation:
```
let string_from_str = ex_str.to_string();
// or
let string_from_str2 = String::from(ex_str);

// Dereference to convert from String to str
let str_from_string: &str = &ex_string;
```

Concat Strings:
```
let a = String::from("a");
let b = String::from("b");

# LHS of concat (+) must be String, second can be &str, so we have to deref b to convert from String to &str
let concat = a + &b;
```

String Indexing / Slicing:
```
// endpoint of range is not inclusive
let str_from_substring: &str = &ex_string[2..4]; // "ll"
```


## Important Traits 

* Copy - Marks types whose values can be duplicated by simply copying bits. This behavior is not overloadable (unlike Clone).

By default, datatypes have move semantics:
```
#[derive(Debug)]
struct Foo;

let x = Foo;

let y = x;

// println!("{:?}", x); // Causes error. Cannot use x now since it has been moved
```

You can give a variable copy semantics so that the bytes get copied over when an assignment occurs, this means that the original value is still usable:
```
// Have to also derive Clone since it's a super trait of Copy
#[derive(Debug, Copy, Clone)]
struct Foo;

let x = Foo;

let y = x;

println!("{:?}", x); // This is okay since y is only a copy of x
```
Note: For a struct to be `Copy`, all of its members must also be `Copy`

* Clone - A copy happens implicitly as part of an assignment like `let y = x`, but a clone happens explicitly when `.clone()` is called.
For example, `String`'s .clone() method copies the string data in the heap, whereas a simple copy would only copy the pointers. Hence, String is `Clone`, but not `Copy`.

* Debug - Enables printing / string formatting of a data type.

## Pattern Matching
https://doc.rust-lang.org/book/ch18-03-pattern-syntax.html
Syntax:
```
match value_var {
    Pattern1(inner_element) => some_operation(inner_element),
    Pattern2 => some_other_operation(),
    _ => println!("No pattern matched!")
}
```

For Option types, it's verbose to pattern match when we know that a type should be `Some`, so we can use `option_val.unwrap()` to get the inner element. This will panic if the value is actually `None` though.
You can also use if let statements: `if let Some(value) = some_function_that_returns_an_option() {... // code in this block only executes if the pattern was matched ...}`

## Multithreading 
* Multithreading - running parts of your program / process code simulataneously
    * Potential issues
        * Deadlock - 2 threads wait on each other to finish using a resource preventing either from making progress
        * Race Condition - threads access data / resources in an inconsistent order
    * Green thread - An implementation of threads by a programming language (as opposed to by the operating system)
* Using thread::spawn to create threads:

```
use std::thread;
use std::time::Duration;

fn main() {
    thread::spawn(|| {
        for i in 1..10 {
            println!("hi number {} from the spawned thread!", i);
            thread::sleep(Duration::from_millis(1));
        }
    });

    for i in 1..5 {
        println!("hi number {} from the main thread!", i);
        thread::sleep(Duration::from_millis(1));
    }
}
```

* A spawned thread ends when the main thread does even if its in the middle of computation
* thread::sleep forces a thread to stop execution and yields control so that another thread can run.
* `join` handles - `thread::spawn` returns a `JoinHandle` which we can call join on to wait for the thread to finish
    * `handle.join.unwrap()` or `thread::JoinHandle::join(join_handle);`    
    * calling `join` blocks the current thread from running until the handle's thread terminates
    * joining multiple threads can be done by mapping the join function across all of the join handles. This should always take as long as the longest running thread.
    * 
