# trait
```
fn main() {
    let article = Article {
        headline: String::from("Rust is awesome!"),
        location: String::from("Internet"),
        author: String::from("John Doe"),
        content: String::from(
            "Rust is a systems programming language that runs blazingly fast and prevents segfaults.",
        ),
    };
    notify(&article);

    let result = some_function("Hello", vec![1, 2, 3]);
    println!("Result of some_function: {}", result);
}

pub trait Summary {
    fn summarize(&self) -> String;
}

pub struct Article {
    pub headline: String,
    pub location: String,
    pub author: String,
    pub content: String,
}

impl Summary for Article {
    fn summarize(&self) -> String {
        format!("{}, by {} ({})", self.headline, self.author, self.location)
    }
}

fn notify<T: Summary>(item: &T) {
    println!("Breaking news! {}", item.summarize());
}
```

## where 
```
use std::fmt::{Debug, Display};

fn main() {
    let user = User {
        name: "Alice".to_string(),
        age: 30,
    };
    let customer = Customer {
        id: 1,
        name: "Bob".to_string(),
    };

    let result = total_length(user.clone(), customer.clone());
    println!("Total length: {}", result);
}

#[derive(Clone)]
struct User {
    name: String,
    age: u32,
}

impl Display for User {
    fn fmt(&self, f: &mut std::fmt::Formatter<'_>) -> std::fmt::Result {
        write!(f, "User {{ name: {}, age: {} }}", self.name, self.age)
    }
}

#[derive(Clone, Debug)]
struct Customer {
    id: u32,
    name: String,
}

fn total_length<T, U>(t: T, u: U) -> i32
where
    T: Display + Clone,
    U: Clone + Debug,
{
    let len_t = format!("{}", t).len() as i32;
    let len_u = format!("{:?}", u).len() as i32;
    len_t + len_u
}
```
