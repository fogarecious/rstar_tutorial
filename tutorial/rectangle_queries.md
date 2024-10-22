# Rectangle Queries

We can obtain all the objects that are completely contained inside a given rectangle.
However, instead of using [Rectangle](https://docs.rs/rstar/latest/rstar/primitives/struct.Rectangle.html), we use [AABB](https://docs.rs/rstar/latest/rstar/struct.AABB.html) to describe a rectangle.

```rust
AABB::from_corners((0, 0), (2, 2))
```

Then, we use [locate_in_envelope](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.locate_in_envelope) to retrieve the objects.

```rust
tree.locate_in_envelope(&AABB::from_corners((0, 0), (2, 2)))
```

The compete code is as follows:

```rust
use rstar::{primitives::Line, RTree, AABB};

fn main() {
    let line1 = Line::new((0, 0), (1, 1));
    let line2 = Line::new((1, 1), (3, 3));
    let line3 = Line::new((3, 3), (4, 4));
    let tree = RTree::bulk_load(vec![line1, line2, line3]);

    for l in tree.locate_in_envelope(&AABB::from_corners((0, 0), (2, 2))) {
        println!("{:?}", l);
    }
}
```

Output:

```text
Line { from: (0, 0), to: (1, 1) }
```

To further include all the objects that are partially contained in the given rectangle, we use [locate_in_envelope_intersecting](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.locate_in_envelope_intersecting).

```rust
use rstar::{primitives::Line, RTree, AABB};

fn main() {
    let line1 = Line::new((0, 0), (1, 1));
    let line2 = Line::new((1, 1), (3, 3));
    let line3 = Line::new((3, 3), (4, 4));
    let tree = RTree::bulk_load(vec![line1, line2, line3]);

    for l in tree.locate_in_envelope_intersecting(&AABB::from_corners((0, 0), (2, 2))) {
        println!("{:?}", l);
    }
}
```

Output:

```text
Line { from: (1, 1), to: (3, 3) }
Line { from: (0, 0), to: (1, 1) }
```

Both methods above have their corresponding mutable version: [locate_in_envelope_mut](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.locate_in_envelope_mut) and [locate_in_envelope_intersecting_mut](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.locate_in_envelope_intersecting_mut).

:arrow_right:  Next: [Tree Intersections](./tree_intersections.md)

:blue_book: Back: [Table of contents](./../README.md)
