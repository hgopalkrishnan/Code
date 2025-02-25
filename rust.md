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



## String


## String slice
The type that signifies “string slice” is written as `&str`


# Control Flows



# Ownership, References, Borrowing, Slicing

- You can have only one mutable reference to a value in a given scope. This prevents _data race_ condition
- We also cannot have a mutable reference while we have an immutable one to the same value. This is because Users of an immutable reference don’t expect the value to suddenly change out from under them!
- Multiple immutable references are allowed because no one who is just reading the data has the ability to affect anyone else’s reading of the data.
- A reference’s scope starts from where it is introduced and continues through the last time that reference is used
