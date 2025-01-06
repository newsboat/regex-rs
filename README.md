# regex-rs: safe wrapper for [POSIX regular expressions API][regex-h] (provided by libc on POSIX-compliant OSes)

[regex-h]: https://pubs.opengroup.org/onlinepubs/9699919799.2008edition/basedefs/regex.h.html#tag_13_37

Example usage:

```rust
use regex_rs::*;

let pattern = "This( often)? repeats time and again(, and again)*\\.";
let compilation_flags = CompFlags::EXTENDED;
let regex = Regex::new(pattern, compilation_flags)
    .expect("Failed to compile pattern as POSIX extended regular expression");

let input = "This repeats time and again, and again, and again.";
// We're only interested in the first match, i.e. the part of text
// that's matched by the whole regex
let max_matches = 1;
let match_flags = MatchFlags::empty();
let matches = regex
    .matches(input, max_matches, match_flags)
    .expect("Error matching input against regex");

// Found a match
assert_eq!(matches.len(), 1);

// Match spans from the beginning to the end of the input
assert_eq!(matches[0].start_pos, 0);
// `end_pos` holds one-past-the-end index
assert_eq!(matches[0].end_pos, input.len());
```

## License

regex-rs is licensed under [the MIT
license](https://opensource.org/licenses/MIT); see the LICENSE file.
