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

## String and String slice

The type that signifies “string slice” is written as `&str`


```Rust
fn main(){
    println!("Hello World");
    let mut s1 = String::from("hello, world");
    println!("length of {s1} is {0}", calc_len(&s1));
    let first_space_idx = first_word_1(&s1);
    println!("The first word is {0}",&s1[0..first_space_idx]);
    
    s1.clear(); //original string deleted by this or some other process 
    //even then the index is preserved
    println!("The index of first space is {first_space_idx}");

    //the following just exits without any effect, perhaps error 
    //println!("The first word is {0}",&s1[0..first_space_idx]);
    
    
    s1 = String::from("hello, world");
    println!("Using string slices, the first word is {0}",first_word_2(&s1));



   s1 = String::from("the following just prints an empty string even if index is valid");
    let mut idx:usize = 0;
    let slen:usize = s1.len();
    println!("init length is {slen}");
    let mut word2 = first_word_3(&s1[idx..slen]);
    while idx<slen {
        word2 = first_word_3(&s1[idx..]);
        println!("{0}",word2);
        idx = idx + word2.len()+1;
    }

}

fn calc_len(s:&String)->usize{
    return s.len();
}

fn next_word(s:&str)->(usize, &str){

    let as_bytes = s.as_bytes();
    for (i,&ch) in as_bytes.iter().enumerate(){
       if ch==b' '{
            println!("found word {0} at {i}" ,&s[..i]);
           return (i,&s[..i]);
       }
    }
    return (s.len(),&s[..]);
}

fn first_word_1(s:&String)->usize{
    let as_bytes = s.as_bytes();
    for (i,&ch) in as_bytes.iter().enumerate(){
       if ch==b' '{
           return i;
       }
    }
    return s.len();
}


fn first_word_2(s:&String)->&str{
    let as_bytes = s.as_bytes();
    for (i,&ch) in as_bytes.iter().enumerate(){
       if ch==b' '{
           return &s[..i];
       }
    }

    return &s[..];
}


fn first_word_3(s:&str)->&str{
    let as_bytes = s.as_bytes();
    for (i,&ch) in as_bytes.iter().enumerate(){
       if ch==b' '{
           return &s[..i];
       }
    }

    return &s[..];
}


```

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
