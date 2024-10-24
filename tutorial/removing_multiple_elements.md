# Removing Multiple Elements

There are three types of removing methods to remove multiple elements from an [RTree](https://docs.rs/rstar/latest/rstar/struct.RTree.html).
The first is [drain](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.drain).

```rust
tree.drain()
```

It is the corresponding removing method of [Element Iterations](./element_iterations.md).

```rust
use rstar::RTree;

fn main() {
    let mut tree = RTree::bulk_load(vec![(0, 0), (1, 2), (8, 5)]);

    for point in tree.drain() {
        println!("{:?}", point);
    }

    println!("Points in the tree:");
    for point in &tree {
        println!("{:?}", point);
    }
}
```

Output:

```text
(0, 0)
(8, 5)
(1, 2)
Points in the tree:
```

The second is [drain_within_distance](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.drain_within_distance).

```rust
tree.drain_within_distance((3, 3), 20)
```

It is the corresponding removing method of [Range Queries](./range_queries.md).

```rust
use rstar::RTree;

fn main() {
    let mut tree = RTree::bulk_load(vec![(0, 0), (1, 2), (8, 5)]);

    for point in tree.drain_within_distance((3, 3), 20) {
        println!("{:?}", point);
    }

    println!("Points in the tree:");
    for point in &tree {
        println!("{:?}", point);
    }
}
```

Output:

```text
(0, 0)
(1, 2)
Points in the tree:
(8, 5)
```

The third is [drain_in_envelope](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.drain_in_envelope) (and [drain_in_envelope_intersecting](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.drain_in_envelope_intersecting)).

```rust
tree.drain_in_envelope(AABB::from_corners((0, 0), (2, 2)))
```

It is the corresponding removing method of [Rectangle Queries](./rectangle_queries.md).

```rust
use rstar::{primitives::Line, RTree, AABB};

fn main() {
    let line1 = Line::new((0, 0), (1, 1));
    let line2 = Line::new((1, 1), (2, 2));
    let line3 = Line::new((2, 2), (3, 3));
    let mut tree = RTree::bulk_load(vec![line1, line2, line3]);

    for element in tree.drain_in_envelope(AABB::from_corners((0, 0), (2, 2))) {
        println!("{:?}", element);
    }

    println!("Lines in the tree:");
    for element in &tree {
        println!("{:?}", element);
    }
}
```

Output:

```text
Line { from: (0, 0), to: (1, 1) }
Line { from: (1, 1), to: (2, 2) }
Lines in the tree:
Line { from: (2, 2), to: (3, 3) }
```

Similarly, [drain_in_envelope_intersecting](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.drain_in_envelope_intersecting) is the corresponding removing method of [locate_in_envelope_intersecting](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.locate_in_envelope_intersecting).

<!-- :arrow_right:  Next:  -->

:blue_book: Back: [Table of contents](./../README.md)
