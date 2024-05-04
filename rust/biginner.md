# how to use print and debug
```
#[derive(Debug)]
struct User {
    name: String,
    age: u32,
    tag: Tag,
}

#[derive(Debug)]
struct Tag {
    name: String,
    value: String,
}

fn main() {
    let value = "This is sample text";
    println!("sample text: {}", value);

    let john = User {
        name: String::from("John"),
        age: 30,
        tag: Tag {
            name: String::from("tag1"),
            value: String::from("value1"),
        },
    };
    println!(
        "His name is {name}, age is {age}, tag name is {tag}, tag value is {value}",
        name = john.name,
        age = john.age,
        tag = john.tag.name,
        value = john.tag.value
    );

    // need to use #[derive(Debug)] to use println! with struct
    println!("use: {:?}", john)
}
```