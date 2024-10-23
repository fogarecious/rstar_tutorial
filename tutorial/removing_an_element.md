# Removing An Element

There are mainly three methods to remove an element in [RTree](https://docs.rs/rstar/latest/rstar/struct.RTree.html).
The first is [remove](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.remove).

```rust
tree.remove(&(1, 2));
```

It is the corresponding removing method of [Existence Queries](./existence_queries.md).

```rust
use rstar::RTree;

fn main() {
    let mut tree = RTree::bulk_load(vec![(0, 0), (1, 2), (8, 5)]);

    tree.remove(&(1, 2));

    for point in &tree {
        println!("{:?}", point);
    }
}
```

Output:

```text
(8, 5)
(0, 0)
```

The second is [pop_nearest_neighbor](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.pop_nearest_neighbor).

```rust
tree.pop_nearest_neighbor(&(0, 0));
```

It is the corresponding removing method of [Nearest Neighbor Queries](./nearest_neighbor_queries.md).

```rust
use rstar::RTree;

fn main() {
    let mut tree = RTree::bulk_load(vec![(1, 1), (2, 2)]);

    tree.pop_nearest_neighbor(&(0, 0));

    for point in &tree {
        println!("{:?}", point);
    }
}
```

Output:

```text
(2, 2)
```

The third is [remove_at_point](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.remove_at_point).

```rust
tree.remove_at_point(&(1.5, 1.5));
```

It is the corresponding removing method of [Shooting Elements](./shooting_elements.md).

```rust
use rstar::{primitives::Rectangle, RTree};

fn main() {
    let rect1 = Rectangle::from_corners((0., 0.), (1., 1.));
    let rect2 = Rectangle::from_corners((1., 1.), (2., 2.));
    let rect3 = Rectangle::from_corners((2., 2.), (3., 3.));
    let mut tree = RTree::bulk_load(vec![rect1, rect2, rect3]);

    tree.remove_at_point(&(1.5, 1.5));

    for rect in &tree {
        println!("{:?}", rect);
    }
}
```

Output:

```text
Rectangle { aabb: AABB { lower: (2.0, 2.0), upper: (3.0, 3.0) } }
Rectangle { aabb: AABB { lower: (0.0, 0.0), upper: (1.0, 1.0) } }
```

These methods all only remove at most one element and return the removed element if any.

<!-- :arrow_right:  Next:  -->

:blue_book: Back: [Table of contents](./../README.md)
