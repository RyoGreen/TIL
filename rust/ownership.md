# rust ownership

```
fn main() {
    let s1 = String::from("hello");
    let s2 = s1;
    // ownership is moved to s2
    // println!("{}, world!", s1);
    println!("{}, world!", s2);
        
    // use close()
    let s3 = s2.clone();
    println!("{}, world!", s2);
    println!("{}, world!", s3);
}
```

### ownership and function
```
fn main() {
    let s1 = String::from("hello");
    takes_ownership(s1);
    // s1 ownership is moved to takes_ownership function
    // println!("{}", s1);
}

fn takes_ownership(some_string: String) {
    println!("{}", some_string);
}
```

```
fn main() {
    let s1 = String::from("hello");
    let (s2, len) = new_string(s1);
    println!("The length of '{}' is {}", s2, len);
    // println!("{}", s1,)
}

fn new_string(s: String) -> (String, usize) {
    let length = s.len();
    (s, length)
}
```
