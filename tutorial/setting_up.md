# Setting Up

First of all, we create a [Cargo](https://doc.rust-lang.org/cargo/index.html) project,

```sh
cargo new my_project
```

where `my_project` is the name of the project.
In the project directory, we add [*rstar*](https://github.com/georust/rstar) to the project.

```sh
cargo add rstar
```

The dependencies in `Cargo.toml` file should look like this:

```toml
[dependencies]
rstar = "0.12.0"
```

<!-- :arrow_right:  Next:  -->

:blue_book: Back: [Table of contents](./../README.md)
