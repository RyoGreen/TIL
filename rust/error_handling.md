# rust error handling
```
use std::error::Error;
use std::io;

fn main() {
    match error_handling("not_correct_key".to_string()) {
        Ok(_) => println!("Success"),
        Err(e) => println!("Error: {}", e),
    }

    match error_handling("hash_key".to_string()) {
        Ok(_) => println!("Success"),
        Err(e) => println!("Error: {}", e),
    }

    match error_handling_dyn("not_correct_key".to_string()) {
        Ok(_) => println!("Success"),
        Err(e) => println!("Error: {}", e),
    }
}

fn error_handling(keyword: String) -> Result<String, io::Error> {
    if keyword == "hash_key" {
        Ok("Success".to_string())
    } else {
        Err(io::Error::new(
            io::ErrorKind::InvalidInput,
            "Error: Invalid key",
        ))
    }
}

fn error_handling_dyn(keyword: String) -> Result<(), Box<dyn Error>> {
    error_handling(keyword)?;
    Ok(())
}
```
