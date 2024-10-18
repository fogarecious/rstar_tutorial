# Associating Data

We can associate points, lines, or rectangles with a custom data.
We use [GeomWithData](https://docs.rs/rstar/latest/rstar/primitives/struct.GeomWithData.html) to define new types that contain our custom data.

```rust
type PointWithName = GeomWithData<(i32, i32), String>;
```

The example defines a new type `PointWithName` that associates a point with a `String`.
Then we can use this type to construct objects that can be searched later.

The complete code is presented below:

```rust
use rstar::{primitives::GeomWithData, RTree};

fn main() {
    type PointWithName = GeomWithData<(i32, i32), String>;

    let p1 = PointWithName::new((0, 0), "A".into());
    let p2 = PointWithName::new((2, 1), "B".into());

    let tree = RTree::bulk_load(vec![p1, p2]);

    println!("{:?}", tree.nearest_neighbors(&(2, 2)));
}
```

Output:

```text
[GeomWithData { geom: (2, 1), data: "B" }]
```

:arrow_right:  Next: [Shooting Elements](./shooting_elements.md)

:blue_book: Back: [Table of contents](./../README.md)
