# cargo-minify

Remove unused code from your Rust programs. Primarily aimed at generated code (prime example: bindings generated by bindgen),
but also usable in more general context.

## Limitations

* Public functions and types in libraries (which makes sense) but also in examples are not considered unused, as well as code that
  is explicitly allowed to be unused (using `#[allow(unused)]`).
* `cargo check` (which `cargo minify` uses in the background) occasionally ignores unused definitions for some reason

## Usage

After installation using `cargo install`, you can run this tool by simply typing `cargo minify` from
your crate root.  This runs it on your project and will print out any changes that will be made to your code.

To actually apply these changes, you have to run `cargo minify --apply`.

You can perform a more precise minifcation by using the `--ignore` option, followed by a
wildcard specification. Unused code in the excluded files will not be touched. You can also you
the `--kinds` flag to specify which types of unused code to remove. Supported are:

* `FUNCTION`, which will remove unused function defintions
* `ASSOCIATED_FUNCTION`, which will remove unused associated functions from `impl` blocks
* `STRUCT`, `ENUM`, `UNION`, which will remove unused type definitions of said type
* `TYPE_ALIAS`, which removes unused type aliases
* `CONST`, which will remove unused constants
* `STATIC`, which will remove unused static variables

Without any `--kinds` specification, all of the above will be removed.

`cargo minify --apply` expects your files to be under control of version control; if this is not
the case a warning will be given and no changes will be made; this can be overridden using the
`--allow-no-vcs`, `--allow-dirty`, and `--allow-staged` flags.

Of course you can also view this information (and other options) by running `cargo minify --help`.

## Future work

Still to add to `cargo minify`:

* Remove unused `static` variables.
* Detected and remove unused derived traits.

## License

Licensed under either of

* Apache License, Version 2.0
  ([LICENSE-APACHE](LICENSE-APACHE) or http://www.apache.org/licenses/LICENSE-2.0)
* MIT license
  ([LICENSE-MIT](LICENSE-MIT) or http://opensource.org/licenses/MIT)

at your option.

## Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted for inclusion in the work by you, as
defined in the Apache-2.0 license, shall be dual licensed as above, without any additional terms or conditions.
