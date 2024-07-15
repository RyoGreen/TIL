# arrange guess game

```
use rand::Rng;
use std::cmp::Ordering;
use std::io;

const MAX_LOOP_NUMBER: u32 = 10;
fn main() {
    let secret_number = rand::thread_rng().gen_range(1..101);
    println!("The secret number is: {}", secret_number);

    for i in 0..MAX_LOOP_NUMBER {
        println!("Please input your guess.");
        let mut guess = String::new();
        match io::stdin().read_line(&mut guess) {
            Ok(_) => {}
            Err(err) => {
                println!("Failed to read line! Error: {}", err);
                return;
            }
        }

        println!("You guessed: {}", guess);

        let guess: u32 = match guess.trim().parse() {
            Ok(num) => num,
            Err(err) => {
                println!("Please enter a valid number! Error: {}", err);
                return;
            }
        };

        match guess.cmp(&secret_number) {
            Ordering::Less => println!("Too small!"),
            Ordering::Greater => println!("Too big!"),
            Ordering::Equal => {
                println!(
                    "You win!\nThe secret number is: {} and your guess is: {}",
                    secret_number, guess
                );
                return;
            }
        }
        println!("You have {} chances left", MAX_LOOP_NUMBER - i - 1)
    }
}
```