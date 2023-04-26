# Samsclass.info Notes
---

# Mapping
- Run Web Spider
- robots.txt
- User-directed spidering (Burp passive spidering)



## URL Encoding
- URLs may contain only printable ASCII characters
  - 0x20 to 0x7e, inclusive
- To transfer other characters, or problematic ASCII characters over HTTP, they must be URL-encoded
```
%3d =
%25 %
%20 space
%oa new line
%00 null byte
```

A further encoding to be aware of is the + character, which represents a URL-encoded space (in addition to the %20 representation of a space.



## Unicode Encoding
- Supports all the world's writing systems
- 16 bits per character, starting with %u

```
%u2215 /
%u8352 é
```

## UTF-8 Encoding
- Variable length
- Uses % character before each byte
- Unicode and UTF-8 are often used to bypass filters in attacks

```
%c2%a9 ©
%e2%89@a0 ≠
```
