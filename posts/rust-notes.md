---
title: Rust notes
date: 2020-11-15
tags:
  - notes
layout: layouts/post.njk
---

A list of questions that I encountered while learning rust. Noting them here for quicker access in the future!

- What is `#[derive(Debug)]` in front of some complex structs e.g. tuple?

https://doc.rust-lang.org/stable/rust-by-example/hello/print/print_debug.html

- Difference between `Debug` and `Display`

https://doc.rust-lang.org/stable/rust-by-example/hello/print/print_display.html

Note that implementing `fmt::Display` will also automatically provide `to_string` functionality.

```rust
use std::fmt;

#[derive(Debug)]
struct Complex {
    real: f64,
    imag: f64,
}

impl fmt::Display for Complex {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // `f` is a buffer, and this method must write the formatted string into it
        write!(f, "{} + {}i", self.real, self.imag)
    } 
}

fn main() {
    let complex = Complex { real: 3.3, imag: 7.2 };
    println!("Compare complex:");
    println!("Display: {}", complex);
    println!("Debug: {:?}", complex);
}
```
```
// Output
Compare complex:
Display: 3.3 + 7.2i
Debug: Complex { real: 3.3, imag: 7.2 }
```

- What is `..` when used before a struct e.g. `let bottom_right = Point { x: 5.2, ..point };`
  
https://doc.rust-lang.org/book/ch05-01-defining-structs.html#creating-instances-from-other-instances-with-struct-update-syntax

- How to destructure structs

https://doc.rust-lang.org/stable/rust-by-example/custom_types/structs.html

- `mod xxx` vs `use xxx` 

https://dev.to/hertz4/rust-module-essentials-12oi

- How to type cast

https://doc.rust-lang.org/stable/rust-by-example/types/cast.html

- `from` vs `into` traits

https://doc.rust-lang.org/stable/rust-by-example/conversion/from_into.html

- Understanding `if let`

https://doc.rust-lang.org/stable/rust-by-example/flow_control/if_let.html