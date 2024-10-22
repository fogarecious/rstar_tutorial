# Tree Intersections

If we have two [RTree](https://docs.rs/rstar/latest/rstar/struct.RTree.html)s, we can compare the objects from each tree and see if they have intersections.
The method [intersection_candidates_with_other_tree](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.intersection_candidates_with_other_tree) outputs all pairs of objects that come from both trees and have intersection with each other.

```rust
tree1.intersection_candidates_with_other_tree(&tree2)
```

The complete code is shown below:

```rust
use rstar::{primitives::Rectangle, RTree};

fn main() {
    let rect11 = Rectangle::from_corners((0, 0), (2, 2));
    let rect12 = Rectangle::from_corners((2, 2), (4, 4));
    let tree1 = RTree::bulk_load(vec![rect11, rect12]);

    let rect21 = Rectangle::from_corners((1, 1), (3, 3));
    let rect22 = Rectangle::from_corners((3, 3), (5, 5));
    let tree2 = RTree::bulk_load(vec![rect21, rect22]);

    for pair in tree1.intersection_candidates_with_other_tree(&tree2) {
        println!("{:?}", pair.0);
        println!("{:?}", pair.1);
        println!();
    }
}
```

Output:

```text
Rectangle { aabb: AABB { lower: (2, 2), upper: (4, 4) } }
Rectangle { aabb: AABB { lower: (3, 3), upper: (5, 5) } }

Rectangle { aabb: AABB { lower: (2, 2), upper: (4, 4) } }
Rectangle { aabb: AABB { lower: (1, 1), upper: (3, 3) } }

Rectangle { aabb: AABB { lower: (0, 0), upper: (2, 2) } }
Rectangle { aabb: AABB { lower: (1, 1), upper: (3, 3) } }

```

Note that the intersections are checked by comparing the bounding boxes of the objects instead of comparing their real geometries.

<!-- :arrow_right:  Next:  -->

:blue_book: Back: [Table of contents](./../README.md)
