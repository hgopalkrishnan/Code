# Concepts
blocks of code evaluate to the last expression in them, and numbers by themselves are also expressions. In this case, the value of the whole if expression depends on which block of code executes. This means the values that have the potential to be results from each arm of the if must be the same type



# Variables, Constants, Data Types, Shadowing & Mutability

## Integer Types
We have integers ranging from 8 bit to 128 bits, signed as well as unsigned, the anotation symbols for declaration are
- Signed: `i8, i16, i32, i64, i128`
- Unsigned: `u8, u16, u32, u64, u128`

There are also architecture dependent integer types `isize` and `usize`. On a 32 bit sisyem these integers are 32 bits wide and on 64 bit systems they are 64 bit sized.  
These are usually used for indexing on the respective machines.


## Floating point Types
- Denoted by `f32` and `f64` for 32 and 64 bit numbers. 
- Floats are always signed.
- Default is 64 bit.

## Boolean type
Specified using `bool` and such variables can take one of two values `true` or `false`.

## String


## String slice
The type that signifies “string slice” is written as `&str`


# Control Flows

## If-else


- Braces after the condition and before the else are mandatory
- Parentheses around condition are not necessary. Compiler gives a warning.
```Rust
fn main() {
  let number = 5;
  if (number%4==0){  
      println!("Number is divisible by 4");
  }else if(number%3==0){
      println!("Number is divisible by 3");
  }
  else if(number%2==0){
      println!("Number is divisible by 2");
  }else{
      println!("The Number is not divisible by 4, 3 or 2");
  }
}
```

### Using if in a let statement
if is an expression not a statement. So it will have a value and that value can be assigned to a variable. This also means that the values returned by each block should be of the same type, so that compiler can determine the type.

```
let condition = true;
let number = if condition {5} else {6};

```


## Loops


### loop




```



```



# Ownership, References, Borrowing, Slicing

- You can have only one mutable reference to a value in a given scope. This prevents _data race_ condition
- We also cannot have a mutable reference while we have an immutable one to the same value. This is because Users of an immutable reference don’t expect the value to suddenly change out from under them!
- Multiple immutable references are allowed because no one who is just reading the data has the ability to affect anyone else’s reading of the data.
- A reference’s scope starts from where it is introduced and continues through the last time that reference is used
