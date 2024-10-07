# Inserting One Element At A Time

To insert an element to the tree, we can use [insert](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.insert).

```rust
tree.insert((1, 2));
```

The complete code is shown below:

```rust
use rstar::RTree;

fn main() {
    let mut tree = RTree::new();
    
    tree.insert((0, 0));
    tree.insert((1, 2));
    tree.insert((8, 5));

    for element in &tree {
        println!("{:?}", element);
    }
}
```

Output:

```text
(8, 5)
(1, 2)
(0, 0)
```

In the example, the elements in the tree are of type `(i32, i32)`.
We can build an [RTree](https://docs.rs/rstar/latest/rstar/struct.RTree.html) to store other types of elements.
The acceptable types include tuples with length up to `9` as well as arrays.
The tuples and arrays can contain integers and floating-point numbers.
In general, an [RTree](https://docs.rs/rstar/latest/rstar/struct.RTree.html) can store elements of type [RTreeObject](https://docs.rs/rstar/latest/rstar/trait.RTreeObject.html).

:arrow_right:  Next: [Inserting Elements In A Batch](./inserting_elements_in_a_batch.md)

:blue_book: Back: [Table of contents](./../README.md)
