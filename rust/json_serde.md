# hot to use serde_json to parse json in rust

```
use serde::Deserialize;
use std::fs;

#[derive(Debug, Deserialize)]
struct Content {
    name: String,
    description: String,
}

fn main() {
    let input = fs::read_to_string("sample.json").expect("Unable to read file");
    let content: Content = serde_json::from_str(&input).expect("Unable to parse json");
    println!(
        "name: {},description: {}",
        content.name, content.description
    );
}
```


sample.json
```
{
    "name": "name",
    "description": "description"
}
```
