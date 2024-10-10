# Nearest Neighbor Queries

To find the nearest neighbor of a given point, we can use [nearest_neighbor](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.nearest_neighbor).
Here is an example:

```rust
use rstar::RTree;

fn main() {
    let tree = RTree::bulk_load(vec![(0, 0), (1, 2), (8, 5)]);

    println!("{:?}", tree.nearest_neighbor(&(3, 3)));
}
```

Output:

```text
Some((1, 2))
```

The distances of points are computed by [PointDistance::distance_2](https://docs.rs/rstar/latest/rstar/trait.PointDistance.html#tymethod.distance_2).

The method [nearest_neighbor](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.nearest_neighbor) returns at most one point.
If it is possible to have more than one nearest neighbor, we can use [nearest_neighbors](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.nearest_neighbors).
For example:

```rust
use rstar::RTree;

fn main() {
    let tree = RTree::bulk_load(vec![(1, 1), (3, 3)]);

    println!("{:?}", tree.nearest_neighbors(&(2, 2)));
}
```

Output:

```text
[(1, 1), (3, 3)]
```

Calling [nearest_neighbor](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.nearest_neighbor) in the example will only return one of `(1, 1)` and `(3, 3)`.

:arrow_right:  Next: [Nearest Neighbor Iterations](./nearest_neighbor_iterations.md)

:blue_book: Back: [Table of contents](./../README.md)
