# rust-clipboard
rust-clipboard is a cross-platform library for getting and setting the contents of the OS-level clipboard.
It has been tested on Windows, Mac OSX, and GNU/Linux.
It is used in Mozilla Servo.


## Prerequisites

On Linux you need the x11 library, install it with something like:

```bash
sudo apt-get install xorg-dev
```

## Example

```rust
fn example() {
    let mut ctx = ClipboardContext::new().unwrap();
    println!("{}", ctx.get_contents());
    ctx.set_contents("some string".to_owned());
}
```

## API

The `ClipboardProvider` trait has the following functions:
```rust
fn new() -> Result<Self, Box<Error>>;
fn get_contents(&mut self) -> Result<String, Box<Error>>;
fn set_contents(&mut self, String) -> Result<(), Box<Error>>;
```

`ClipboardContext` a type alias for one of {`WindowsClipboardContext`, `OSXClipboardContext`, `X11ClipboardContext`, `NopClipboardContext`}, all of which implement `ClipboardProvider`. Which concrete type is chosen for `ClipboardContext` depends on the OS (via conditional compilation).

## License
Since the x11 backend contains code derived from xclip (which is GPLv2), rust-clipboard must currently be treated as GPLv2.
I plan to rewrite `x11_clipboard.rs` by strictly referencing the ICCCM standard, and relicense to Apache2.
All the other code in `rust-clipboard` may be treated as Apache2.