# Variables
We can declare variables with let.
let binds variables.
Binding is the process of associating a variable name with a value.
Variables can refer to the value bound to them.
If the value bound to the variable is changed, the variable can refer to the changed value.
It is similar to assignment in other languages. However, Rust separates binding and assignment as different concepts.

## Immutable variables
We can not change the value of immutable variables.

Example of general variable declaration using let
```rust
fn main() {
  let x = 5; // x refers to 5
  println!("x is {}", x);　// x is 5
  x = 6; // Error, can not reassign
}
```

## Mutable variables
Becuase immutable variables are less likely to cause unexpected bugs and increase readability.
However, immutable variables can not be reused.
We can make variables mutable by using the mut keyword when declaring variables.

let mut variable_name = value;

Example of making variables mutable using mut
```rust
fn main() {
  let mut x = 5; // x refers to 5
  println!("x is {}", x);　// x is 5
  x = 6; // OK, x refers to 6
  println!("x is {}", x);　// x is 6
}
```

## Shadowing
We can redefine variables by declaring variables with the same name.
Variable redefinition is limited to cases where the variable scope is different.
The variable scope is the range where the variable is valid.
In essence, we can change the value of the variable without using mut. (※ The variable is not mutable)
```rust
fn main() {
  let x = 5; // x refers to 5
  println!("x is {}", x);　// x is 5
  let x = 6; // Redefine x as 6
  println!("x is {}", x);　// x is 6
}
```

# Constants
Constants are bound in the same way as variables.
Constants are declared using const.
A type annotation is required when declaring a constant.
Unlike variables, constants can not change the value bound to them. (mut can not be used)
```rust
const MAX_POINTS: i32 = 100000;
```