# Rectangles

We can store [Rectangle](https://docs.rs/rstar/latest/rstar/primitives/struct.Rectangle.html)s in [RTree](https://docs.rs/rstar/latest/rstar/struct.RTree.html).
A [Rectangle](https://docs.rs/rstar/latest/rstar/primitives/struct.Rectangle.html) can be defined by two corners.

```rust
let rect1 = Rectangle::from_corners((0., 0.), (1., 1.));
```

The complete code is shown below:

```rust
use rstar::{primitives::Rectangle, RTree};

fn main() {
    let rect1 = Rectangle::from_corners((0., 0.), (1., 1.));
    let rect2 = Rectangle::from_corners((1., 1.), (2., 2.));
    let rect3 = Rectangle::from_corners((2., 1.), (4., 3.));

    let tree = RTree::bulk_load(vec![rect1, rect2, rect3]);

    for rect in tree.nearest_neighbor_iter_with_distance_2(&(1.5, 1.5)) {
        println!("{:?}", rect);
        println!("{:?}", rect.0.nearest_point(&(1.5, 1.5)));
    }
}
```

Output:

```text
(Rectangle { aabb: AABB { lower: (1.0, 1.0), upper: (2.0, 2.0) } }, 0.0)
(1.5, 1.5)
(Rectangle { aabb: AABB { lower: (2.0, 1.0), upper: (4.0, 3.0) } }, 0.25)
(2.0, 1.5)
(Rectangle { aabb: AABB { lower: (0.0, 0.0), upper: (1.0, 1.0) } }, 0.5)
(1.0, 1.0)
```

In the example, we list all the rectangles with both [nearest_points](https://docs.rs/rstar/latest/rstar/primitives/struct.Rectangle.html#method.nearest_point) and distance to a given point.

Similar to points, rectangles can be constructed in high dimensions.

:arrow_right:  Next: [Associating Data](./associating_data.md)

:blue_book: Back: [Table of contents](./../README.md)
