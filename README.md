# Simple *rstar* Tutorial

[*rstar*](https://github.com/georust/rstar) is an implementation of [R<sup>*</sup>-tree](https://en.wikipedia.org/wiki/R*-tree).
The data structure stores spatial data such as points and lines efficiently.
This tutorial serves as a quick start for [*rstar*](https://github.com/georust/rstar).
We try to keep each part of the tutorial as simple as possible.

(The tutorial is for *rstar* version `0.12.0`.)

## Contents

* [Setting Up](./tutorial/setting_up.md)
* [Number Of Elements](./tutorial/number_of_elements.md)
* [Element Iterations](./tutorial/element_iterations.md)
* Insertion
  * [Inserting One Element At A Time](./tutorial/inserting_one_element_at_a_time.md)
  * [Inserting Elements In A Batch](./tutorial/inserting_elements_in_a_batch.md)
* Useful Queries
  * [Existence Queries](./tutorial/existence_queries.md)
  * [Nearest Neighbor Queries](./tutorial/nearest_neighbor_queries.md)
  * [Nearest Neighbor Iterations](./tutorial/nearest_neighbor_iterations.md)
  * [Range Queries](./tutorial/range_queries.md)
* Data Types
  * [Points](./tutorial/points.md)
  * [Lines](./tutorial/lines.md)
  * [Rectangles](./tutorial/rectangles.md)
  * Associating Data
* Other Queries
  * Finding Elements
  * Rectangle Queries
  * Tree Intersections
* Removal
  * Removing An Element
  * Removing Multiple Elements
* Support For Serde
* Custom Data Types

## See Also

* [*rstar*](https://github.com/georust/rstar) - the spatial index.
* [R<sup>*</sup>-tree](https://en.wikipedia.org/wiki/R*-tree) - an explanation of R<sup>*</sup>-tree.

## Contributions

Pull requests for typos, incorrect information, or other ideas are welcome!

## License

All code in the tutorial is provided under the MIT License.
