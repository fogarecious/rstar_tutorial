# Element Iterations

Another way to see elements in the tree is through iterations.
Here is an example:

```rust
use rstar::RTree;

fn main() {
    let tree: RTree<(i32, i32)> = RTree::new();
    for element in &tree {
        println!("{:?}", element);
    }
}
```

We can also use [iter](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.iter) and [iter_mut](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.iter_mut) to obtain an (mutable) iteration of the elements in the tree.

:arrow_right:  Next: [Inserting One Element At A Time](./inserting_one_element_at_a_time.md)

:blue_book: Back: [Table of contents](./../README.md)
