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

## map_err
```rust
use std::fs::File;
use std::io::Read;

#[derive(Debug)]
enum CustomError {
    Io(String),
    Unknown(String),
}

fn main() {
    match read_username_from_file("file.txt") {
        Ok(username) => println!("Username: {}", username),
        Err(e) => println!("Error: {:?}", e),
    }
}

fn read_username_from_file(path: &str) -> Result<String, CustomError> {
    let mut file = File::open(path).map_err(|e| CustomError::Io(e.to_string()))?;

    let mut s = String::new();
    file.read_to_string(&mut s)
        .map_err(|e| CustomError::Unknown(e.to_string()))?;

    Ok(s)
}
```

## from
```rust
use std::fs::File;
use std::io::{self, Read};

#[derive(Debug)]
enum CustomError {
    Io(String),
}

impl From<io::Error> for CustomError {
    fn from(e: io::Error) -> Self {
        CustomError::Io(e.to_string())
    }
}

fn main() {
    match read_username_from_file("file.txt") {
        Ok(username) => println!("Username: {}", username),
        Err(e) => println!("Error: {:?}", e),
    }
}

fn read_username_from_file(path: &str) -> Result<String, CustomError> {
    let mut file = File::open(path)?;

    let mut s = String::new();
    file.read_to_string(&mut s)?;

    Ok(s)
}
```
