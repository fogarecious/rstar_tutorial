# Shooting Elements

We can find elements that are located at a given point or containing that point.
This can be done by using [locate_at_point](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.locate_at_point).

In the following example, we find the rectangle that contains the point `(1.5, 1.5)`.

```rust
use rstar::{primitives::Rectangle, RTree};

fn main() {
    let rect1 = Rectangle::from_corners((0., 0.), (1., 1.));
    let rect2 = Rectangle::from_corners((1., 1.), (2., 2.));
    let rect3 = Rectangle::from_corners((2., 2.), (3., 3.));

    let tree = RTree::bulk_load(vec![rect1, rect2, rect3]);

    println!("{:?}", tree.locate_at_point(&(1.5, 1.5)));
}
```

Output:

```text
Some(Rectangle { aabb: AABB { lower: (1.0, 1.0), upper: (2.0, 2.0) } })
```

There are variants of [locate_at_point](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.locate_at_point):

* [locate_at_point_mut](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.locate_at_point_mut) - the returned element can be mutated.
* [locate_all_at_point](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.locate_all_at_point) - it returns multiple elements if there are more than one.
* [locate_all_at_point_mut](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.locate_all_at_point_mut) - all the returned elements can be mutated.

<!-- :arrow_right:  Next:  -->

:blue_book: Back: [Table of contents](./../README.md)
