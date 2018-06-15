# 📦✨  wasm-pack
> Your favorite rust -> wasm workflow tool!

[![Build Status](https://travis-ci.org/ashleygwilliams/wasm-pack.svg?branch=master)](https://travis-ci.org/ashleygwilliams/wasm-pack)
[![Build status](https://ci.appveyor.com/api/projects/status/7jjuo5wewu9lyyfi?svg=true)](https://ci.appveyor.com/project/ashleygwilliams/wasm-pack)

This tool seeks to be a one-stop shop for building and working with rust-
generated WebAssembly that you would like to interop with JavaScript, in the
browser or with Node.js. `wasm-pack` helps you build and publish rust-generated
WebAssembly to the npm registry to be used alongside any other javascript
package in workflows that you already use, such as a bundler like
[webpack] or [greenkeeper].

[bundler-support]: https://github.com/rustwasm/team/blob/master/goals/bundler-integration.md#details
[webpack]: https://webpack.js.org/
[greenkeeper]: https://greenkeeper.io/

This project is a part of the [rust-wasm] group. You can find more info by
visiting that repo!

[rust-wasm]: https://github.com/rustwasm/team

![demo](demo.gif)

## 🔮 Prerequisities

- [Development Environment](docs/prerequisites.md)
- [Installation and Getting Started](docs/setup.md)

## 🎙️ Commands

- [`init`](docs/init.md): Generate an npm wasm pkg from a rustwasm crate
- [`pack`](docs/pack.md): Create a tarball of your rustwasm pkg
- [`publish`](docs/publish.md): Publish your rustwasm pkg to a registry

## 📝 Logging

We generate a `wasm-pack.log` file if `wasm-pack` errors on you, and you can
customize the log verbosity using the verbosity flag.

| Verbosity     | Result                                              |
| ------------- |-----------------------------------------------------|
| -v            | All Info, Warn, and Errors are logged               |
| -vv           | All Debug, Info, Warn, and Errors are logged        |
| -vvv          | All Trace, Debug, Info, Warn, and Errors are logged |

## 👯 Contributing

Read our [guide] on getting up and running for developing `wasm-pack`, and
check out our [contribution policy].

[guide]: docs/contributing.md
[contribution policy]: CONTRIBUTING.md

## ⚡ Quickstart Guide

1. Write a crate in Rust.
2. Add `wasm-bindgen` to your `Cargo.toml`:

  ```toml
  [lib]
  crate-type = ["cdylib"]

  [dependencies]
  wasm-bindgen = "0.2"
  ```
3. Add this to the top of your `src/lib.rs`:

  ```rust
  #![feature(proc_macro, wasm_import_module, wasm_custom_section)]

  extern crate wasm_bindgen;

  use wasm_bindgen::prelude::*;
  ```

4. Annotate your public functions with `#[wasm_bindgen]`, for example:

  ```rust
  #[wasm_bindgen]
  extern {
      fn alert(s: &str);
  }

  #[wasm_bindgen]
  pub fn greet(name: &str) {
      alert(&format!("Hello, {}!", name));
  }
  ```

5. Install this tool: `cargo install wasm-pack`
6. Run `wasm-pack init`, optionally, pass a path to a dir or a scope (see above for details)
7. This tool generates files in a `pkg` dir
8. To publish to npm, run `wasm-pack publish`. You may need to login to the
  registry you want to publish to. You can login using `wasm-pack login`.`

[rust-wasm/36]: https://github.com/rustwasm/team/issues/36
[wasm-bindgen]: https://github.com/alexcrichton/wasm-bindgen
