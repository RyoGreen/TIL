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

