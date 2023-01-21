# Pattern Matching

The `match` keyword let you match a value against one or more _patterns_. The
comparisons are done from top to bottom and the first match wins.

The patterns can be simple values, similarly to `switch` in C and C++:

```rust,editable
fn main() {
    let input = 'x';

    match input {
        'q'                   => println!("Quitting"),
        'a' | 's' | 'w' | 'd' => println!("Moving around"),
        '0'..='9'             => println!("Number input"),
        _                     => println!("Something else"),
    }
}
```

Unlike `switch`, Rust pattern matching must be _exhaustive_, in other words
cover all possible cases.

The `_` pattern is a wildcard pattern which matches any value. It can be used
to handle all cases not explicitly covered and produce an _exhaustive_ match statement.
