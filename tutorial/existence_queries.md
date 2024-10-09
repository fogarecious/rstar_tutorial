# Existence Queries

We can use [contains](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.contains) to decide whether a point is already inserted to the tree or not.
Here is an example:

```rust
use rstar::RTree;

fn main() {
    let tree = RTree::bulk_load(vec![(0, 0), (1, 2), (8, 5)]);

    println!("{}", tree.contains(&(1, 2)));
    println!("{}", tree.contains(&(100, 100)));
}
```

Output:

```text
true
false
```

:arrow_right:  Next: [Nearest Neighbor Queries](./nearest_neighbor_queries.md)

:blue_book: Back: [Table of contents](./../README.md)
