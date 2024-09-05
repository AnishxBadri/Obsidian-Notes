
- The main function is always the first code that runs in every executable Rust program.
- In `println!("Hello, world!")`,  `!` represents that it is a macro, without the exclamation mark it would denote a function
- Cargo is Rust’s build system and package manager. 
- In Rust, packages are referred to as crates.
- cargo new for creating a project. cargo build for building a project. cargo run for running a project. cargo check to build a project without producing a binary to check for errors using cargo check. When finally ready to release project run cargo build –release this is slower in compile time but performs all optimizations possible.
- In Rust, variables are immutable by default. We add mut before the variable to make it mutable. But constants are still immutable.
- In the line let mut guess = String::new(); The :: syntax in the ::new line indicates that new is an associated function of the String type. An associated function is a function that’s implemented on a type, in this case String. Therefore the above line has created a mutable variable that is currently bound to a new empty instance of a String.
- A match expression is made up of arms. An arm consists of a pattern to match against, and the code that should be run if the value given to match fits that arm’s pattern. Rust takes the value given to match and looks through each arm’s pattern in turn.
- Constants are valid for the entire time a program runs within the scope in which they were declared.
- Constants can only be declared in any scope, including the global scope.
- Constants may be set only to a constant expression, not the result of a value that could only be computed at runtime.
- Shadowing:

```rust
fn main() {       
  let x = 5;         
  let x = x + 1;         
  {           
    let x = x * 2;           
    println!("The value of x in the inner scope is:  {x}");       
  }         
  println!("The value of x is: {x}");   
}
```

- X is first bound to 5, then new x is created and is bound to value of 6. Then in inner scope it is shadowed  and prints 12 and then outside the scope it is back to 6.
- Difference between shadowing and mut is that since we are effectively creating a new variable when using let, we change the type of the value but reuse the same name.

```rust
let spaces = "   ";   
let spaces = spaces.len(); 

// This is fine.  
// But the below will result in a compile time error for mismatched types  
  
let mut spaces = "   ";   
spaces = spaces.len();
```
- Every value in Rust is of a certain data type. Rust is a statically typed language. 
- A scalar type represents a single value. Rust has four primary scalar types: integers, floating-point numbers, Booleans and characters.
- Integers are numbers without a fractional component. Integers have various variants like u32, u8, i8, i32, etc. Rust by default uses i32.
- Rust includes checks for integer overflow in debug mode that causes your program to panic at runtime if this behavior. Panicking in rust is when a program exits with an error. But in release mode it performs two’s complement wrapping, basically wraps around.
- Floating-point types:
- Rust also has two primitive types for floating-point numbers which are numbers with decimal points. 
- The two types are f32 and f64.
- Boolean type has two possible values: true and false. They are one byte sized.
- The Character Type:
- Rust’s char type is the languages most primitive alphabetic type. Char literals are specified with single quotes and string literals are with double quotes. Rust’s char type is four bytes in size and represents a Unicode scalar value, which means it can represent a lot more than just ASCII. Accented letters; Chinese, Japanese, and Korean characters; emoji; and zero-width spaces are all valid char values in Rust. Unicode scalar values range from U+0000 to U+D7FF and U+E000 to U+10FFFF inclusive. 
- Compound types can group multiple values into one type. Two primitive compound types are tuples and arrays.
- Tuple is a general way of grouping together a number of values with a variety of types into one compound type with a fixed length.
	- To get induvidual values we have to pattern match and destructure.
	- The tuple without any values has a special name, unit. This value and its corresponding type are both written `()` and represent an empty value.
- Array is a collection of multiple values with the same type and fixed length.
	- This is useful when you want data allocated on the stack rather than the heap.
	- Very useful when you know the number of elements will not change.
	- `let a: [i32; 5] = [1, 2, 3, 4, 5];`
	- or  `let a = [3; 5];` creates an array of 5 three's.
	- Accessed through normal indexing.
	- Invalid index access results in a runtime error and the main thread panics, since rust in runtime checks if index is less than length. memory sagety in action
- Rust uses snake case for function and variable names.
- In rust function signatures, you must declare the type of each parameter.
- Function bodies are made of series of statements optionally ending in an expression. Rust is an expression-based language.
	- Statements are instructions that perform some action and do not return a value. Expressions evaluate to a resultant value.
	- Creating a variable and assigning a a value to it with `let` is a statement.
	- Function definitions are also statements.
	- Statements do not return values. Therefore, you can’t assign a let statement to another variable
	- Expressions evaluate to a value and make up most of the rest of the code that you'll write in Rust. A math operation like `5+6` which evaluates to `11` can be part of statements.
	- Expressions can be part of statements. The `6` in the statement `let y = 6;` is an expressions that evaluates to the value `6`. 
	- ```fn main() {  
		❶ let y = {❷
		let x = 3; ❸ x+1
		};
		println!("The value of y is: {y}");
		}``` . here 2 is expression block bound to y as part of statement 1. Line without a semicolon at the end 3 is an expression.
		Expressions do not include ending semicolons.
	- If you add a semicolon to the end of an expression, you turn it into a statement, and it will then not return a value.
- Functions can return early from a function by using the `return` keyword and specifying a value, but most functions return the last expression implicitly.
- For if conditions, unlike other languages rust will not automatically try to convert non-Boolean types to a Boolean.
- Ifs are expressions. That means each arm of if has to be of the same type.
- 

