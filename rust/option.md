## rust option

- simple option example
```rust
fn main() {
    let option = simple_option(100);
    match option {
        Some(n) => println!("{}", n),
        None => println!("None"),
    }
}

fn simple_option(n: i32) -> Option<i32> {
    if n == 0 {
        return None;
    }
    Some(n)
}
```

- option with map
```rust
fn main() {
    let option = simple_option(0);
    let result = option.map(|n| n * 2).unwrap_or(10);
    println!("{}", result)
}

fn simple_option(n: i32) -> Option<i32> {
    if n == 0 {
        return None;
    }
    Some(n)
}
```

- checking Option
```rust
fn main() {
    let option = simple_option(0);
    if option.is_some() {
        println!("Not Some")
    }
}

fn simple_option(n: i32) -> Option<i32> {
    if n == 0 {
        return None;
    }
    Some(n)
}
```
