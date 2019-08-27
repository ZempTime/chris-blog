---
title: Snippet - Nifty Way of Text -> Data
description: Got hit by an "oh cool!" moment and had to document it.
date: 2019-08-27
tags:
  - snippet
  - rust
layout: layouts/post.njk
---

I'm gonna share some code, and at the start, it might look like gibberish. But something pretty cool is happening in [here](https://github.com/BurntSushi/advent-of-code/blob/master/aoc03/src/main.rs):

```rust
impl FromStr for Claim {
    type Err = Box<Error>;

    fn from_str(s: &str) -> Result<Claim> {
        lazy_static! {
            static ref RE: Regex = Regex::new(r"(?x)
                \#
                (?P<id>[0-9]+)
                \s+@\s+
                (?P<x>[0-9]+),(?P<y>[0-9]+):
                \s+
                (?P<width>[0-9]+)x(?P<height>[0-9]+)
            ").unwrap();
        }

        let caps = match RE.captures(s) {
            None => return err!("unrecognized claim"),
            Some(caps) => caps,
        };
        Ok(Claim {
            id: caps["id"].parse()?,
            x: caps["x"].parse()?,
            y: caps["y"].parse()?,
            width: caps["width"].parse()?,
            height: caps["height"].parse()?,
        })
    }
}
```

This code is supposed to turn a structured string into meaningfully usable data. This is from problem 3 of advent-of-code 2018, where you're trying to draw different "claims" on a large grid. The rest of the problem isn't important, only that we're trying to draw things and ask questions about a 1000x1000ish grid. Once you know this, you can understand what the data means. The input looks like this:

```
#1 @ 257,829: 10x23
#2 @ 902,685: 10x20
#3 @ 107,733: 20x25
#4 @ 186,421: 20x11
#5 @ 360,229: 29x10
#6 @ 362,248: 24x10
#7 @ 922,250: 13x26
#8 @ 256,742: 18x14
...
```

### The Cool Part

Did you notice?

```rust
// the regex is structured to store certain matches, like 'id' here:
(?P<id>[0-9]+)

// so they can be later referenced like this:
id: caps["id"].parse()?,
```

That's _sweet!_

### Other notes:

That `lazy_static!` stuff is recommended by the [regex readme](https://crates.io/crates/regex):

> It is an anti-pattern to compile the same regular expression in a loop since compilation is typically expensive. (It takes anywhere from a few microseconds to a few milliseconds depending on the size of the regex.) Not only is compilation itself expensive, but this also prevents optimizations that reuse allocations internally to the matching engines.
>
> In Rust, it can sometimes be a pain to pass regular expressions around if they're used from inside a helper function. Instead, we recommend using the lazy_static crate to ensure that regular expressions are compiled exactly once.

So basically, it's a fancy way to ensure the regular expression is only compiled once.
