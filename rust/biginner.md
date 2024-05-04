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

# array and slice
```
fn main() {
    // array
    let xs: [i32; 5] = [1, 2, 3, 4, 5];
    for x in xs.iter() {
        println!("{}", x);
    }

    // slice
    let slice = &xs[1..3];
    println!("{:?}", slice);

    // create slice from vec
    let mut points: Vec<Point> = Vec::new();
  
    // how to append to slice
    let p = Point { x: 1, y: 1 };
    points.push(p);
    for point in points.iter() {
        println!("x: {}, y: {}", point.x, point.y);
    }

    let mut value = Vec::<i8>::with_capacity(10);
    value.push(3);
    value.push(4);
    for v in &value {
        println!("{}", v);
    }
}

struct Point {
    x: i32,
    y: i32,
}
```
