# Custom Data Types

We can implement our own objects that can be inserted into an [RTree](https://docs.rs/rstar/latest/rstar/struct.RTree.html).
To do this, we declare a struct and make it implement [RTreeObject](https://docs.rs/rstar/latest/rstar/trait.RTreeObject.html).

```rust
struct Circle {
    center: (f64, f64),
    radius: f64,
}

impl RTreeObject for Circle {
    type Envelope = /**/;

    fn envelope(&self) -> Self::Envelope {
        /**/
    }
}
```

In the implementation, we have to specify precisely the associated type, [Envelope](https://docs.rs/rstar/latest/rstar/trait.RTreeObject.html#associatedtype.Envelope).
Since our `Circle` is 2-dimensional, we use `AABB<(f64, f64)>` here.

```rust
type Envelope = AABB<(f64, f64)>;
```

Then, we implement the function, [envelope](https://docs.rs/rstar/latest/rstar/trait.RTreeObject.html#tymethod.envelope), to describe how we would like to cover our `Circle`.

```rust
fn envelope(&self) -> Self::Envelope {
    let p1 = (self.center.0 - self.radius, self.center.1 - self.radius);
    let p2 = (self.center.0 + self.radius, self.center.1 + self.radius);
    AABB::from_corners(p1, p2)
}
```

Finally, we can use [locate_in_envelope](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.locate_in_envelope) to find our `Circle`.

The complete code is shown below:

```rust
use rstar::{RTree, RTreeObject, AABB};

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

fn main() {
    let c1 = Circle {
        center: (1., 1.),
        radius: 0.5,
    };
    let c2 = Circle {
        center: (2., 2.),
        radius: 0.5,
    };
    let c3 = Circle {
        center: (3., 3.),
        radius: 0.5,
    };
    let tree = RTree::bulk_load(vec![c1, c2, c3]);

    for c in tree.locate_in_envelope(&AABB::from_corners((1., 1.), (3., 3.))) {
        println!("{:?}", c);
    }
}
```

Output:

```text
Circle { center: (2.0, 2.0), radius: 0.5 }
```

:arrow_right:  Next: [Custom Distances](./custom_distances.md)

:blue_book: Back: [Table of contents](./../README.md)
