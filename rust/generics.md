# Generics
```rust
fn main() {
    let number_list = vec![1, 2, 3, 4, 5];
    let result = largest_i32(&number_list);
    println!("The largest number is {}", result);
    let char_list = vec!['a', 'b', 'c', 'd', 'e'];
    println!("The largest char is {}", largest_char(&char_list));
    let number_list = vec![34, 50, 25, 100, 65];
    let result = largest(&number_list);
    println!("The largest number is {}", result);
}

fn largest_i32(list: &[i32]) -> i32 {
    let mut largest = list[0];

    for &item in list.iter().skip(1) {
        if item > largest {
            largest = item;
        }
    }

    largest
}

fn largest_char(list: &[char]) -> &char {
    let mut largest = &list[0];

    for item in list.iter().skip(1) {
        if item > largest {
            largest = item
        }
    }
    largest
}

fn largest<T: Ord>(list: &[T]) -> &T {
    let mut largest_num = &list[0];

    for item in list.iter().skip(1) {
        if item > largest_num {
            largest_num = item
        }
    }
    largest_num
}
```
