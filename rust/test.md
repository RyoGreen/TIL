# test
```
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    fn can_hold(&self, other: &Rectangle) -> bool {
        self.width > other.width && self.height > other.height
    }
}

fn add_two(a: i32) -> i32 {
    a + 2
}

fn check_positive(a: i32) -> Result<i32, String> {
    if a > 0 {
        Ok(a)
    } else {
        Err(String::from("a must be greater than 0"))
    }
}

#[cfg(test)]
mod tests {
    use super::*;
    #[test]
    fn larget_can_hold_smaller() {
        let larger = Rectangle {
            width: 8,
            height: 7,
        };
        let smaller = Rectangle {
            width: 5,
            height: 1,
        };
        assert!(larger.can_hold(&smaller))
    }

    #[test]
    fn check_positive_works() {
        assert_eq!(check_positive(5), Ok(5));
        assert_eq!(
            check_positive(-3),
            Err(String::from("a must be greater than 0"))
        );
    }
}
```

