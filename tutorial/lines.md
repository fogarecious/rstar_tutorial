# Lines

[RTree](https://docs.rs/rstar/latest/rstar/struct.RTree.html) can store [Line](https://docs.rs/rstar/latest/rstar/primitives/struct.Line.html)s.
A [Line](https://docs.rs/rstar/latest/rstar/primitives/struct.Line.html) consists of two points.

```rust
let line1 = Line::new((0., 0.), (0., 2.));
```

The code above constructs a line starting from `(0., 0.)` and ending at `(0., 2.)`.

Here is the complete example:

```rust
use rstar::{primitives::Line, RTree};

fn main() {
    let line1 = Line::new((0., 0.), (0., 2.));
    let line2 = Line::new((1., 0.), (3., 0.));
    let line3 = Line::new((2., 0.), (0., 2.));
    
    let tree = RTree::bulk_load(vec![line1, line2, line3]);

    for li in tree.nearest_neighbor_iter_with_distance_2(&(1., 1.)) {
        println!("{:?}", li);
    }
}
```

Output:

```text
(Line { from: (2.0, 0.0), to: (0.0, 2.0) }, 0.0)
(Line { from: (1.0, 0.0), to: (3.0, 0.0) }, 1.0)
(Line { from: (0.0, 0.0), to: (0.0, 2.0) }, 1.0)
```

The example above lists all the lines sorted by their distance to point `(1., 1.)`.
The distance is computed by [nearest_point](https://docs.rs/rstar/latest/rstar/primitives/struct.Line.html#method.nearest_point).

We can obtain the length of a line by [length_2](https://docs.rs/rstar/latest/rstar/primitives/struct.Line.html#method.length_2), which returns the distance between the line's [from](https://docs.rs/rstar/latest/rstar/primitives/struct.Line.html#structfield.from) point and [to](https://docs.rs/rstar/latest/rstar/primitives/struct.Line.html#structfield.to) point.

Similar to points, lines can be constructed in high dimensions.

<!-- :arrow_right:  Next:  -->

:blue_book: Back: [Table of contents](./../README.md)
