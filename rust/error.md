# Error

## match
```rust
fn main() {
    let f = File::open("hello.txt");
    let _ = match f {
        Ok(file) => file,
        Err(error) => {
            panic!("{:?}", error)
        }
    };
}
```

## expect
```rust
fn main() {
    let f = File::open("hello.txt").expect("Failed to open hello.txt");
}
```
