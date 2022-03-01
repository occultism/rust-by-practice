# Reference and Borrowing

### Reference
🌟
```rust,editable

fn main() {
   let x = 5;
   // fill the blank
   let p = __;

   println!("the memory address of x is {:p}", p); // output: 0x16fa3ac84
}
```

🌟
```rust,editable

fn main() {
    let x = 5;
    let y = &x;

    // modify this line only
    assert_eq!(5, y);
}
```

🌟
```rust,editable

// fix error
fn main() {
    let mut s = String::from("hello, ");

    borrow_object(s)
}

fn borrow_object(s: &String) {}
```

🌟
```rust,editable

// fix error
fn main() {
    let mut s = String::from("hello, ");

    borrow_object(&s)
}

fn borrow_object(s: &mut String) {}
```

🌟🌟
```rust,editable

fn main() {
    let mut s = String::from("hello, ");

    // fill the blank to make it work
    let p = __;
    
    p.push_str("world");
}
```

#### ref
`ref` can be used to take references to a value, similar to `&`.

🌟🌟🌟
```rust,editable

fn main() {
    let c = '中';

    let r1 = &c;
    // fill the blank，dont change other code
    let __ r2 = c;

    assert_eq!(*r1, *r2);
    
    // check the equality of the two address strings
    assert_eq!(get_addr(r1),get_addr(r2));
}

// get memory address string
fn get_addr(r: &char) -> String {
    format!("{:p}", r)
}
```

### Borrowing rules
🌟
```rust,editable

// remove something to make it work
// don't remove a whole line !
fn main() {
    let mut s = String::from("hello");

    let r1 = &mut s;
    let r2 = &mut s;

    println!("{}, {}", r1, r2);
}
```

#### Mutablity
🌟 Error: Borrow a immutable object as mutable
```rust,editable

fn main() {
    //fix error by modifying this line
    let  s = String::from("hello, ");

    borrow_object(&mut s)
}

fn borrow_object(s: &mut String) {}
```

🌟🌟 Ok: Borrow a mutable object as immutable
```rust,editable

// this code has no errors!
fn main() {
    let mut s = String::from("hello, ");

    borrow_object(&s);
    
    s.push_str("world");
}

fn borrow_object(s: &String) {}
```

### NLL
🌟🌟
```rust,editable

// comment one line to make it work
fn main() {
    let mut s = String::from("hello, ");

    let r1 = &mut s;
    r1.push_str("world");
    let r2 = &mut s;
    r2.push_str("!");
    
    println!("{}",r1);
}
```

🌟🌟🌟
```rust,editable

fn main() {
    let mut s = String::from("hello, ");

    let r1 = &mut s;
    let r2 = &mut s;

    // add one line below to make a compiler error: cannot borrow `s` as mutable more than once at a time
    // you can't use r1 and r2 at the same time
}
```