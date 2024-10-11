# Nearest Neighbor Iterations

We can use [nearest_neighbor_iter](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.nearest_neighbor_iter) to obtain a sequence of points sorted by distances to a given point.
Here is an example:

```rust
use rstar::RTree;

fn main() {
    let tree = RTree::bulk_load(vec![(0, 0), (1, 2), (8, 5)]);

    for point in tree.nearest_neighbor_iter(&(3, 3)) {
        println!("{:?}", point);
    }
}
```

Output:

```text
(1, 2)
(0, 0)
(8, 5)
```

To obtain the distances associated with the output points, we can use [nearest_neighbor_iter_with_distance_2](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.nearest_neighbor_iter_with_distance_2).

```rust
use rstar::RTree;

fn main() {
    let tree = RTree::bulk_load(vec![(0, 0), (1, 2), (8, 5)]);

    for point in tree.nearest_neighbor_iter_with_distance_2(&(3, 3)) {
        println!("{:?}", point);
    }
}
```

Output:

```text
((1, 2), 5)
((0, 0), 18)
((8, 5), 29)
```

The distances are calculated by [PointDistance::distance_2](https://docs.rs/rstar/latest/rstar/trait.PointDistance.html#tymethod.distance_2).

:arrow_right:  Next: [Range Queries](./range_queries.md)

:blue_book: Back: [Table of contents](./../README.md)
