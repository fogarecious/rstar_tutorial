# Points

[RTree](https://docs.rs/rstar/latest/rstar/struct.RTree.html) is able to store points represented by tuples.
We can also store arrays in it.

```rust
use rstar::RTree;

fn main() {
    let mut tree = RTree::new();

    tree.insert([0, 0]);
    tree.insert([1, 2]);
    tree.insert([8, 5]);

    for point in &tree {
        println!("{:?}", point);
    }
}
```

Output:

```text
[8, 5]
[1, 2]
[0, 0]
```

Arrays are useful when the length of points is more than `9`, which is more than the length implemented for tuples.
However, the length of arrays must be fixed, so we cannot store `vec![...]`, which has variable length.

:arrow_right:  Next: [Lines](./lines.md)

:blue_book: Back: [Table of contents](./../README.md)
