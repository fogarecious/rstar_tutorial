# Inserting Elements In A Batch

To insert many elements at a time, we can use [bulk_load](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.bulk_load), which performs more efficiently than executing multiple [insert](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.insert).

```rust
let tree = RTree::bulk_load(vec![(0, 0), (1, 2), (8, 5)]);
```

Note that [bulk_load](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.bulk_load) constructs an [RTree](https://docs.rs/rstar/latest/rstar/struct.RTree.html) directly.
If we need to insert elements later, we can still use [insert](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.insert) on the tree obtained from [bulk_load](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.bulk_load).

The complete code is shown below:

```rust
use rstar::RTree;

fn main() {
    let tree = RTree::bulk_load(vec![(0, 0), (1, 2), (8, 5)]);

    for element in &tree {
        println!("{:?}", element);
    }
}
```

Output:

```text
(8, 5)
(1, 2)
(0, 0)
```

:arrow_right:  Next: [Existence Queries](./existence_queries.md)

:blue_book: Back: [Table of contents](./../README.md)
