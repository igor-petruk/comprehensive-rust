# `Mutex`

[`Mutex<T>`][1] ensures mutual exclusion _and_ allows mutable access to `T`
behind a read-only interface:

```rust,editable
use std::sync::Mutex;

fn main() {
    let v: Mutex<Vec<i32>> = Mutex::new(vec![10, 20, 30]);
    println!("v: {:?}", v.lock().unwrap());

    {
        let v: &Mutex<Vec<i32>> = &v;
        let mut guard = v.lock().unwrap();
        guard.push(40);
    }

    println!("v: {:?}", v.lock().unwrap());
}
```

Notice how we have a [`impl<T: Send> Sync for Mutex<T>`][2] blanket
implementation.

[1]: https://doc.rust-lang.org/std/sync/struct.Mutex.html
[2]: https://doc.rust-lang.org/std/sync/struct.Mutex.html#impl-Sync-for-Mutex%3CT%3E
[3]: https://doc.rust-lang.org/std/sync/struct.Arc.html

<details>

You can get an `&mut T` from an `&Mutex<T>` by taking the lock. The `MutexGuard` ensures that the
`&mut T` doesn't outlive the lock being held.

If a thread panics while holding a mutex then the mutex is 'poisoned', and no other thread is able
to access the data. If the mutex is poisoned then `Mutex::lock` will return an error.

`Mutex<T>` implements both `Send` and `Sync` iff `T` implements `Send`.

</details>
