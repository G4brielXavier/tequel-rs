# Random Number Generator

## Summary

- [Random Number Generator](#random-number-generator)
  - [Summary](#summary)
  - [Time](#time)
    - [`rand_by_nano`](#rand_by_nano)
  - [LGC (Linear Congruential Generator)](#lgc-linear-congruential-generator)
    - [`rand_lgc`](#rand_lgc)
  - [From Hardware/OS](#from-hardwareos)
    - [`rand_deep_string`](#rand_deep_string)
    - [`rand_u32`](#rand_u32)
  - [Range](#range)
    - [`rand_range`](#rand_range)


## Time

### `rand_by_nano`

Generates a combination of random numbers from `SystemTime::subsec_nanos` combined with four constants (`u32`).

```rust
use tequel_rs::rng::TequelRng;

fn main() -> Result<(), Box<dyn std::error::Error>> {

    let tequel_rng: TequelRng = TequelRng::new();

    let rand = tequel_rng.rand_by_nano();

    println!("{}", rand);

    Ok(())

}
```

```bash
2045930856
```


## LGC (Linear Congruential Generator)

### `rand_lgc`

Generates a number from a `seed` delivered as parameter. If `seed` is equal, number will be equal too.

```rust
use tequel_rs::rng::TequelRng;

fn main() -> Result<(), Box<dyn std::error::Error>> {

    let tequel_rng: TequelRng = TequelRng::new();

    let seed: u32 = 2026; // <-- Your seed

    let rand1: u32 = tequel_rng.rand_lgc(seed);
    let rand2: u32 = tequel_rng.rand_lgc(seed);

    println!("NUM1: {}", rand1);
    println!("NUM2: {}", rand2);

    Ok(())

}
```

```bash
NUM1: 77654757
NUM2: 77654757
```


## From Hardware/OS

### `rand_deep_string`


Generates a set of numbers and letters with custom length provided. `getrandom::getrandom` lib + some constants, that is used to get *Network noises*, *Keyboard* and others hardware's information.

```rust
use tequel_rs::rng::TequelRng;

fn main() -> Result<(), Box<dyn std::error::Error>> {

    let tequel_rng: TequelRng = TequelRng::new();

    let rand1: u32 = tequel_rng.rand_deep_string(8); // generates an u32 of 8 bytes

    let rand2: u32 = tequel_rng.rand_deep_string(16); // generates an u32 of 16 bytes

    println!("rand1: {}", rand1);
    println!("rand2: {}", rand2);

    Ok(())

}
```

```bash
rand1: e3016e1fdc8dbe98
rand2: 698fe1747b02f3122b890cf0ea11b6c0
```

### `rand_u32`

Generates a set of random numbers only using `getrandom::getrandom`. 

```rust
use tequel_rs::rng::TequelRng;

fn main() -> Result<(), Box<dyn std::error::Error>> {

    let tequel_rng: TequelRng = TequelRng::new();

    let rand1: u32 = tequel_rng.rand_u32();
    println!("rand1: {}", rand1);

    Ok(())

}
```

```bash
rand1: 4250173843
```


## Range 

### `rand_range`

Generates a number between `min` and `max` using `rand_u32`.


```rust
use tequel_rs::rng::TequelRng;

fn main() -> Result<(), Box<dyn std::error::Error>> {

    let tequel_rng: TequelRng = TequelRng::new();
    let mut r = String::new();

    // I will generate 10 numbers
    for _ in 0..9 {
        // Generate number between 0 and 10
        let n = tequel_rng.rand_weak(0, 10);
        
        let p = format!("{} ", n);
        r.push_str(&p);
    }

    println!("{}", r);

    Ok(())

}
```

```bash
9 2 1 10 9 2 5 2 6
```