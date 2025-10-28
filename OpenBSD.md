# Installing on OpenBSD

Make sure following build dependency packages are installed:
- `llvm`
- `libhidapi`: current packaged version `0.13.1` lacks `get_report_descriptor` functionality that was added later, so will need to fetch ports, bump the version (`0.15.0` works) and build it locally.

Some dependencies require knowledge of `libclang` library paths, so export env before building or installing:

```sh
export LD_LIBRARY_PATH=/usr/local/llvm21/lib
export LIBCLANG_PATH=/usr/local/llvm21/lib/
export CC=/usr/bin/clang
export CXX=/usr/bin/clang++
```

On more recent `rust` might need to allow warnings:

```sh
export RUSTFLAGS="-A warnings"
```

Increase the data limits and build:

```sh
ulimit -d 33554432
cargo build -r
```

Install the required binary crates, e.g.:

```sh
cargo install --path ./cli --locked
cargo install --path ./keygen --locked
cargo install --path ./validator --locked
cargo install --path ./platform-tools-sdk/cargo-build-sbf --locked
```

