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

# Structures

## Basics

```Rust
struct User{
    active:bool,
    username:String,
    email:String,
    sign_in_count:u64
}//notice no semi-colon

fn main(){
    //
    /*
    creating instance of a structure
    notice semicolon at end of `let` statement
    the values are specified by colon(:) not equal-to(=)
    
    
    */
    let user1 = User{
        active:true,
        username:String::from("someusername123"),
        email:String::from("someone@example.com"),
        sign_in_count:0
    };
    
    //access using dot operator is not supported in format string
   // println!("Email of user is:{user1.email}");
   
    println!("Email of user is:{0}",user1.email);

    /*
    creating a mutable instance of a struct
    Note that the whole structure (all fields) become mutable
    individual fields cannot be made (im)mutable
   */
   let mut user2 = User{
       active:true,
       username:String::from("someotheruser"),
       email:String::from("someotherone@example.com"),
       sign_in_count:2
   };
   
    println!("Email of user2 before change is:{0}",user2.email);
   //change a value
   user2.email = String::from("anotheruser@example.com");
   
    println!("Email of user2 after change is:{0}",user2.email);
}    
```
## Returning structs from functions

```Rust
struct User{
    active:bool,
    username:String,
    email:String,
    sign_in_count:u64
}//notice no semi-colon

fn main(){
    //
    /*
    creating instance of a structure
    notice semicolon at end of `let` statement
    the values are specified by colon(:) not equal-to(=)
    
    
    */
    let user1 = build_user(
        String::from("someusername123"),
        String::from("someone@example.com")
    );
    
 
    println!("Email of user1 is:{0}",user1.email);

    /*
    creating a mutable instance of a struct
    Note that the whole structure (all fields) become mutable
    individual fields cannot be made (im)mutable
   */
   
    let mut user2 = build_user_field_init_shorthand(
        String::from("someshorthandusername123"),
        String::from("someshorthandone@example.com")
    );
    
    println!("Email of user2 before change is:{0}",user2.email);
   //change a value
   user2.email = String::from("anotheruser@example.com");
   
    println!("Email of user2 after change is:{0}",user2.email);
}    

//Note: names of parameters are EXACTLY the same as field names
//for which short hand has to be used
fn build_user_field_init_shorthand(username:String, email:String)->User{
    User{
        active:true, 
        username,
        email,
        sign_in_count:0
    }

}



fn build_user(username:String, email:String)->User{
    User{
        active:true, 
        username:username,
        email:email,
        sign_in_count:0
    }
    
    /*
   The above expression (not ending in ;), is same as the statement
   
        let user1=User{
            active:true, 
            username:username,
            email:email,
            sign_in_count=0;
        };
        return user1;
    */
}

```
## Creating new instance of structs



### 'field init shorthand' in a function
https://doc.rust-lang.org/book/ch05-01-defining-structs.html#using-the-field-init-shorthand


```Rust
struct User{
    active:bool,
    username:String,
    email:String,
    sign_in_count:u64
}//notice no semi-colon

fn main(){
    let user2 = build_user_field_init_shorthand(
        String::from("someshorthandusername123"),
        String::from("someshorthandone@example.com")
    );

    println!("Email of user2  is:{0}",user2.email);
}    

//Note: names of parameters are EXACTLY the same as field names
//for which short hand has to be used
fn build_user_field_init_shorthand(username:String, email:String)->User{
    User{
        active:true, 
        username,
        email,
        sign_in_count:0
    }
}

```


### 'struct update' syntax 

The syntax `..` specifies that the remaining fields (of user2) not explicitly set should have the same value as the fields in the given instance(user1).


```Rust

fn main(){
    let user1 = User {
        active: true,
        username: String::from("someusername123"),
        email: String::from("someone@example.com"),
        sign_in_count: 1,
    };
    
    let user3 = User {
        email: String::from("someone@example3.com"),
        ..user2
    };
    
    println!("{0}, {1}",user3.email,user3.username);    
}
```

### Regular method
In below code, we are explicitly setting each field of the instance `user2`, from values of instance `user1` even when only the email has to be updated.

```Rust
fn main(){
    let user1 = User {
        active: true,
        username: String::from("someusername123"),
        email: String::from("someone@example.com"),
        sign_in_count: 1,
    };
     
    let user2 = User {
        active: user1.active,
        username: user1.username,   //Note: being a string, the value is moved. user1.username is now empty
        email: String::from("someone@example2.com"),
        sign_in_count: user1.sign_in_count,
    };

    println!("{0}, {1}",user2.email,user2.username);
}
```


# Ownership, References, Borrowing, Slicing

- You can have only one mutable reference to a value in a given scope. This prevents _data race_ condition
- We also cannot have a mutable reference while we have an immutable one to the same value. This is because Users of an immutable reference don’t expect the value to suddenly change out from under them!
- Multiple immutable references are allowed because no one who is just reading the data has the ability to affect anyone else’s reading of the data.
- A reference’s scope starts from where it is introduced and continues through the last time that reference is used


### Notes for code below
- When we pass mutable/immutable references we have to prefix `&` or `&mut` to the params in the function call
- The function signature type annotation will have prefix `&` or `&mut`
- Inside the function code we can use the variable names with out the prefix `&` or `&mut`
```Rust
fn main(){
    let mut s2 = String::from("hello, ");
    let s1=String::from("world");
    
    append_string(&s1,&mut s2);
    println!("After appending: {s2}");
}

fn append_string(s1:&String, s2:&mut String){
   s2.push_str(s1);
}
```
