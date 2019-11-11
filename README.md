
# Filtered index for Rust [LTS](https://lib.rs/lts)

This is a subset of the crates.io index with the following changes:

 * Crate versions that failed to build with Rust 1.24.0 were removed (almost, it's a work in progress).
   This way even deep dependency trees won't accidentally pull in crates that require a newer version of compiler.
   The index is sitll useful even with older versions of Rust, since there still are going to be fewer problematic crates.

 * Crate versions published before Rust 1.0 release (2015-05) were removed.
   This helps building with `-Z minimal-versions` flag, which is less likely to pick up obsolete and defunct versions.

 * Commit history is squashed for faster cloning.

The index preserves the original crate checksums, uses the same crates.io API, and unmodified crate tarballs from crates.io.

## Usage

Make `.cargo/config` files in your project's directory, with the following content:

```toml
[source.crates-io]
replace-with = 'lts-repo-replacement'

[source.lts-repo-replacement]
registry = 'https://github.com/kornelski/crates.io-index.git'
```

and run `cargo generate-lockfile` or `cargo update`.

Note that it will a generate standard `Cargo.lock` compatible with all Rust versions.
The lockfile will let the project build even without the `.cargo/config` file.
    