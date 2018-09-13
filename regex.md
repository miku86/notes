# Regex

- best practice to write as specific regular expressions as possible: "success" vs "Error: unsuccessful operation"

Expressions:

```
.     // any single character except newline
[a-z] // letters from a to z, lowercase
[A-Z] // letters from a to z, uppercase
\d    // 0-9
\w    // [a-zA-Z0-9_]
\s    // whitespace (space, tab, newline)
[^]   // exclude
.{3,} // 3 or more times any single character
a*    // zero or more a
a+    // one or more a
a?    // optional a
|     // or
()    // capture group to reuse
(\d(\d)) // two captured groups, e.g. 15 and 5
(?:com|de) // non-capturing group
$1    // use first captured group
```

Flags:

```
/g    // find all matches, not only first one
/i    // ignore case
/m    // multiline
```

Further Readings:

- [Regexr](https://regexr.com)
- [Youtube](https://www.youtube.com/playlist?list=PLfdtiltiRHWGRPyPMGuLPWuiWgEI9Kp1w)
