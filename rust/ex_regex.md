# How to use regex in RUST
```
fn main() {
    let re = regex::Regex::new(r"^[\w\.-]+@gmail\.com$").unwrap();

    let correct_email = "example@gmail.com";
    let incorrect_email = "incorrect@amail.com";

    if re.is_match(correct_email) {
        println!("{} is a valid email", correct_email);
    } else {
        println!("{} is not a valid email", correct_email);
    }

    if re.is_match(incorrect_email) {
        println!("{} is a valid email", incorrect_email);
    } else {
        println!("{} is not a valid email", incorrect_email);
    }
}
```
