# Range Queries

Given a point, we can find all the points that are within a distance to the point by [locate_within_distance](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.locate_within_distance).

```rust
tree.locate_within_distance((3, 3), 20);
```

The example finds all the points that are within distance `20` to point `(3, 3)`.

The complete example is shown below:

```rust
use rstar::RTree;

fn main() {
    let tree = RTree::bulk_load(vec![(0, 0), (1, 2), (8, 5)]);

    for point in tree.locate_within_distance((3, 3), 20) {
        println!("{:?}", point);
    }
}
```

Output:

```text
(1, 2)
(0, 0)
```

<!-- :arrow_right:  Next:  -->

:blue_book: Back: [Table of contents](./../README.md)
