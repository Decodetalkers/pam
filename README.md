# pam - Safe Rust API to the Linux Pluggable Authentication Modules (PAM)

[![Crates.io](https://img.shields.io/crates/v/pam-f.svg)](https://crates.io/crates/pam-f)
[![Documentation](https://docs.rs/pam/badge.svg)](https://docs.rs/pam/)
[![License](https://img.shields.io/crates/l/pam.svg?branch=master)](https://travis-ci.org/1wilkens/pam)

Note: Currently only supports basic username/password authentication out-of-the-box.


## Warning
Environment support through the `env` module is probably broken and should not be used in the current state!


## Usage
1. Add `pam` to your Cargo.toml:
```toml
[dependencies]
pam = { package = "pam-f", version = "0.8.1" }
```
2. Use the `Authenticator` struct to authenticate and open a session
```rust
pub fn main() {
        let service = "<yourapp>";
        let user = "<user>";
        let password = "<pass>";

        let mut auth = pam::Authenticator::with_password(service).unwrap();
        auth.handler_mut().set_credentials(user, password);
        if auth.authenticate().is_ok() && auth.open_session().is_ok() {
            println!("Successfully opened a session!");
        }
        else {
            println!("Authentication failed =/");
        }
}
```


## TODO:
  - [x] Implement basic user/password authentication
  - [x] Add `Authenticator` struct
  - [ ] Add (more) documentation
  - [x] Verify current `conv` does not leak memory
  - [x] Allow custom `conv` functions to be passed
  - [ ] Code cleanup


## Supported Rust versions
The library is only continuously built against Rust stable, beta and nightly but as it does not use a lot of new language features it should probably compile on older versions as well.
If you encounter problems building on older versions and a small fix can be applied to make the build succeed, consider opening a pull request.


## Note about stability
This crate follows [semantic versioning](http://semver.org). As such all versions below `1.0.0` should be
considered development versions. This means the API could change any time.


## License

Licensed under either of

 * Apache License, Version 2.0, ([LICENSE-APACHE](LICENSE-APACHE) or http://www.apache.org/licenses/LICENSE-2.0)
 * MIT license ([LICENSE-MIT](LICENSE-MIT) or http://opensource.org/licenses/MIT)

at your option.

### Contribution

Unless you explicitly state otherwise, any contribution intentionally
submitted for inclusion in the work by you, as defined in the Apache-2.0
license, shall be dual licensed as above, without any additional terms or
conditions.
