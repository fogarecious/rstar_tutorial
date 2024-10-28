# Support For Serde

We can save and load an [RTree](https://docs.rs/rstar/latest/rstar/struct.RTree.html) by [serde](https://serde.rs/).
To use [serde](https://serde.rs/), we need to add feature [serde](https://docs.rs/crate/rstar/latest/features#serde) to [rstar](https://docs.rs/rstar/latest/rstar/index.html).

```sh
cargo add rstar -F serde
```

In this tutorial, we use [serde_json](https://docs.rs/serde_json/latest/serde_json/) to do the (de)serialization.

```sh
cargo add serde_json
```

The dependencies in `Cargo.toml` should look like this:

```toml
[dependencies]
rstar = { version = "0.12.0", features = ["serde"] }
serde_json = "1.0.131"
```

Now, we can use [serde_json::to_string_pretty](https://docs.rs/serde_json/latest/serde_json/fn.to_string_pretty.html) and [serde_json::from_str](https://docs.rs/serde_json/latest/serde_json/fn.from_str.html) to save and load an [RTree](https://docs.rs/rstar/latest/rstar/struct.RTree.html).

```rust
use rstar::RTree;

fn main() {
    let tree = RTree::bulk_load(vec![(0, 0), (1, 2), (8, 5)]);

    let json = serde_json::to_string_pretty(&tree).unwrap();
    println!("{}", json);

    let tree2: RTree<(i32, i32)> = serde_json::from_str(&json).unwrap();
    println!("Points in tree2:");
    for point in &tree2 {
        println!("{:?}", point);
    }
}
```

Output:

```text
{
    "root": {
    "children": [
        {
        "Leaf": [
            0,
            0
        ]
        },
        {
        "Leaf": [
            1,
            2
        ]
        },
        {
        "Leaf": [
            8,
            5
        ]
        }
    ],
    "envelope": {
        "lower": [
        0,
        0
        ],
        "upper": [
        8,
        5
        ]
    }
    },
    "size": 3,
    "_params": null
}
Points in tree2:
(8, 5)
(1, 2)
(0, 0)
```

:arrow_right:  Next: [Custom Data Types](./custom_data_types.md)

:blue_book: Back: [Table of contents](./../README.md)
