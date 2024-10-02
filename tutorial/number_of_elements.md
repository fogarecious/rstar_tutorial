# Number Of Elements

To create an R<sup>\*</sup>-tree, we use [RTree::new()](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.new).
Then we can use [size()](https://docs.rs/rstar/latest/rstar/struct.RTree.html#method.size) to obtain the number of elements stored in the R<sup>\*</sup>-tree.

The complete code is presented below:

```rust
use rstar::RTree;

fn main() {
    let tree: RTree<(i32, i32)> = RTree::new();
    println!("{}", tree.size());
}
```

In the code, we assume we are going to store points of type `(i32, i32)`.

Output:

```text
0
```

It outputs `0` because there is no points in the tree.
We will talk about point insertions later.

<!-- :arrow_right:  Next:  -->

:blue_book: Back: [Table of contents](./../README.md)
