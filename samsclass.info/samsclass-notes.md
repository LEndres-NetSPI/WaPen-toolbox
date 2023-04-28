# Samsclass.info Notes
---

# Mapping
- Run Web Spider
- robots.txt
- User-directed spidering (Burp passive spidering)
- Map client and server-side technologies
- Banner grabbing, wappalyzer

# HTTP Headers
- Applications behind a load balancer or proxy may use `X-Forwarded-For` header to identify source
- Can be manipulated by attacker to inject content

# Hack Steps
1. Identify all entry points for user input
- URL, query string parameters, POST data, cookies, HTTP headers
2. Examine query string format; should be some variation on name/value pair
3. Identify any other channels that allow user-controallable or third-party data into the app
4. View HTTP server banner returned by the app; it may use several different servers
5. Check for other software identifiers in custom HTTP headers or HTML source code
6. Run `httprint` to fingerprint the web server
7. Research software versions for vulnerabilities
8. Review map of URLs to find interesting file extensions, directories, etc. with clues about the technologies in use
9. Review names of session tokens to identify technologies being used
10. Use lists of common technologies, or Google, to identify technologies in use, or discover other websites that use the same technologies
11. Google unusual cookie names, scripts, HTTP headers, etc. If possible, download and install the software to analyze it and find vulnerabilities

# Mapping the Attack Surface
- Access controls - horizontal and vertical privilege escalation
- User impersonation functions - privilege escalation
- Cleartext communications - session hijacking, credential theft
- Off-site links - leakage of query string parameters in the Referer header
- Interfaces to external systems - shortcuts handling sessions or access controls

### Other Notes
`http://eis/pub/media/117/view`
Try changing that to `edit`

Mess with all input/parameters and see if you can get a different response
 
# Remember
- NetSPI has a checklist to review, this is your most important material to understand

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
