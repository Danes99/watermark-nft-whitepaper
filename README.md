# White Paper Project Using mdBook

This repository hosts the source files of our white paper, which is created using `mdBook`. `mdBook` is a utility to create modern online books from Markdown files. It's used by the Rust community for most online books, and can be used by anyone looking to create an easily-navigable, readable, and feature-rich online document.

## Prerequisites

Before you can work on this project, you need to have the following software installed on your machine:

- **Rust**: The Rust programming language, which includes `cargo`, Rust's package manager. You can install Rust from the [official website](https://www.rust-lang.org/tools/install).

- **mdBook**: You can install it via `cargo`:

```rust
cargo install mdbook
```

## Project Structure

- **src**: The source Markdown files for each chapter of the book. Each chapter has its own file.

- **book**: The output of the `mdBook` build process. This directory is automatically generated and should not be edited directly.

- **theme**: Contains the theme files used by `mdBook` to generate the book. This includes the HTML, CSS, and JavaScript that forms the reader-facing side of the book.

## Building the Book

You can build the book using the following command:

```rust
mdbook build
```

This will create a `book` directory with the compiled HTML files.

## Serving the Book Locally

For a live-preview of the book, you can use the following command:

```rust
mdbook serve
```

This will serve the book at `http://localhost:3000` (by default) and reload the browser page whenever a change is detected.

## Contributing

Contributions are welcome! Please read our [contributing guide](CONTRIBUTING.md) to learn about our development process, how to propose bugfixes and improvements, and how to build and test your changes.

## License

This project is licensed under the terms of the [MIT license](LICENSE).

If you encounter any problems or have suggestions, please open an issue. We appreciate your feedback!
