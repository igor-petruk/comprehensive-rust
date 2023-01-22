# Deriving Traits

You can let the automatically derive a number of traits at compile time:

```rust,editable
#[derive(Debug, Clone, PartialEq, Eq, Default)]
struct Player {
    name: String,
    strength: u8,
    hit_points: u8,
}

fn main() {
    let p1 = Player::default();
    let p2 = p1.clone();
    println!("Is {:?}\nequal to {:?}?\nThe answer is {}!", &p1, &p2,
             if p1 == p2 { "yes" } else { "no" });
}
```

<details>

* You can implement your own derivation macros just like these. Many libraries do that. This is an advanced topic outside of this course scope.
    
</details>
