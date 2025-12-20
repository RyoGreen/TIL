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

## result
```rust
use std::fs::File;
use std::io::Read;

fn main() {
    let file_path = String::from("file.txt");
    match read_username_from_file(file_path) {
        Ok(username) => println!("Username: {}", username),
        Err(e) => eprintln!("Error reading username: {}", e),
    }
}

fn read_username_from_file(path: String) -> Result<String, std::io::Error> {
    let mut f = File::open(path)?;
    let mut s = String::new();
    f.read_to_string(&mut s)?;
    Ok(s)
}
```
