# Custom Distances

In the previous tutorial, we declared a struct, `Circle`, and made it be an [RTreeObject](https://docs.rs/rstar/latest/rstar/trait.RTreeObject.html).
Then we can insert a `Circle` into an [RTree](https://docs.rs/rstar/latest/rstar/struct.RTree.html).
However, if we call [nearest_neighbor](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.nearest_neighbor) on the [RTree](https://docs.rs/rstar/latest/rstar/struct.RTree.html), we get an error:

```text
error[E0599]: the method `nearest_neighbor` exists for struct `RTree<Circle>`, but its trait bounds were not satisfied
```

To solve this problem, we need to implement [PointDistance](https://docs.rs/rstar/latest/rstar/trait.PointDistance.html) for our `Circle`.

```rust
impl PointDistance for Circle {
    fn distance_2(&self, point: &(f64, f64)) -> f64 {
        /**/
    }
}
```

The `point` parameter in [distance_2](https://docs.rs/rstar/latest/rstar/trait.PointDistance.html#tymethod.distance_2) is of type `&(f64, f64)` because the [Envelope](https://docs.rs/rstar/latest/rstar/trait.RTreeObject.html#associatedtype.Envelope) in our [RTreeObject](https://docs.rs/rstar/latest/rstar/trait.RTreeObject.html) implementation is specified to `AABB<(f64, f64)>`, where `(f64, f64)` in the `AABB<(f64, f64)>` corresponds to the type of `point`.

We use the implementation of [distance_2](https://docs.rs/rstar/latest/rstar/trait.PointDistance.html#tymethod.distance_2) provided by the document of [PointDistance](https://docs.rs/rstar/latest/rstar/trait.PointDistance.html).
Note that the returned value of [distance_2](https://docs.rs/rstar/latest/rstar/trait.PointDistance.html#tymethod.distance_2) must be square of the distance.

The complete code is presented below:

```rust
use rstar::{PointDistance, RTree, RTreeObject, AABB};

#[derive(Debug)]
struct Circle {
    center: (f64, f64),
    radius: f64,
}

impl RTreeObject for Circle {
    type Envelope = AABB<(f64, f64)>;

    fn envelope(&self) -> Self::Envelope {
        let p1 = (self.center.0 - self.radius, self.center.1 - self.radius);
        let p2 = (self.center.0 + self.radius, self.center.1 + self.radius);

        AABB::from_corners(p1, p2)
    }
}

impl PointDistance for Circle {
    fn distance_2(&self, point: &(f64, f64)) -> f64 {
        let d_x = self.center.0 - point.0;
        let d_y = self.center.1 - point.1;
        
        let distance_to_center = (d_x * d_x + d_y * d_y).sqrt();
        let distance_to_ring = distance_to_center - self.radius;
        let distance_to_circle = f64::max(0., distance_to_ring);

        distance_to_circle * distance_to_circle
    }
}

fn main() {
    let c1 = Circle {
        center: (1., 1.),
        radius: 1.,
    };
    let c2 = Circle {
        center: (0., -1.),
        radius: 1.,
    };
    let tree = RTree::bulk_load(vec![c1, c2]);

    for c in tree.nearest_neighbor_iter_with_distance_2(&(0., 0.)) {
        println!("{:?}", c);
    }
}
```

Output:

```text
(Circle { center: (0.0, -1.0), radius: 1.0 }, 0.0)
(Circle { center: (1.0, 1.0), radius: 1.0 }, 0.17157287525381)
```

There are other methods in trait [PointDistance](https://docs.rs/rstar/latest/rstar/trait.PointDistance.html) that we can implement for better efficiency.
For example, [locate_within_distance](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.locate_within_distance) and [drain_within_distance](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.drain_within_distance) uses [PointDistance::distance_2_if_less_or_equal](https://docs.rs/rstar/latest/rstar/trait.PointDistance.html#method.distance_2_if_less_or_equal).
We can override the method to gain more runtime efficiency if possible.

<!-- :arrow_right:  Next:  -->

:blue_book: Back: [Table of contents](./../README.md)
