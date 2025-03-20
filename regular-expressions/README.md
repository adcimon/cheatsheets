# Regular Expressions

[Regular expressions](https://en.wikipedia.org/wiki/Regular_expression) are a particular kind of formal grammar used to parse strings and other textual information that are known as Regular Languages in formal language theory.

## Index

* [Syntax](#syntax)
* [Examples](#examples)
* [References](#references)

## Syntax

| Delimiters | |
| - | - |
| `^` | Start. |
| `$` | End. |
| `/x/` | Start and end. |

| Character Classes | |
| - | - |
| `\d` | Digit. |
| `\w` | Word. |
| `\s` | Whitespace, tab or line break characters. |
| `\D` `^\d` | Not digit. |
| `\W` `^\w` | Not word. |
| `\S` `^\s` | Not whitespace, tab or line break characters. |
| `.` | Any character. |

| Composites | |
| - | - |
| `xy` | `x` followed by `y`. |
| `x\|y` | `x` or `y` (prefer `x`). |

| Quantifiers | |
| - | - |
| `x?` | 0 or 1 (prefer 1). |
| `x+` | 1 or more (prefer more). |
| `x*` | 0 or more (prefer more). |
| `x??` | 0 or 1 (prefer 0). |
| `x+?` | 1 or more (prefer fewer). |
| `x*?` | 0 or more (prefer fewer). |
| `x{n}` | `n`. |
| `x{n,m}` | `n` to `m` (prefer more). |
| `x{n,}` | `n` or more (prefer more). |
| `x{n}?` | `n`. |
| `x{n,m}?` | `n` to `m` (prefer fewer). |
| `x{n,}?` | `n` or more (prefer fewer). |

| Ranges | |
| - | - |
| `a-z` | Letter in range `a-z`. |
| `A-Z` | Letter in range `A-Z`. |
| `0-9` | Digit in range `0-9`. |

| Flags | |
| - | - |
| `/x/g` | Global, find all matches rather than stopping after the first match. |
| `/x/m` | Multi line, `^` and `$` match the start and end of a line. |
| `/x/i` | Case insensitive. |

Characters `^.[$()|*+?` can be used with a backslash `\`.

| Unicode | |
| - | - |
| `/^$/u` | Required to enable unicode mode. |
| `\p{L}` | Unicode letter. |
| `\p{N}` | Unicode number. |
| `\p{M}` | Unicode mark. |

## Examples

Begins with "The".
```
^The
```

Ends with "end".
```
end$
```

`ab` followed by zero or one `c`.
```
abc?
```

`ab` followed by one or more `c`.
```
abc+
```

`ab` followed by zero or more `c`.
```
abc*
```

`ab` followed by two `c`.
```
abc{2}
```

`ab` followed by two up to five `c`.
```
abc{2,5}
```

`ab` followed by two or more `c`.
```
abc{2,}
```

`a` followed by `b` or `c`.
```
a(b|c)
```

`a` followed by zero or more `bc`.
```
a(bc)*
```

`a` followed by two up to five `bc`.
```
a(bc){2,5}
```

A string that doesn't contain characters from `a` to `z` or from `A` to `Z`.
```
[^a-zA-Z]
```

A string that doesn't contain the character `-`.
```
[^-]
```

A string that doesn't contain the characters `<>`.
```
[^<>]
```

A string that can be empty.
```
^(^$)|(<REGEXP>)$
```

Alphanumeric string (e.g. nicknames).
```
^[a-zA-Z]+[a-zA-Z0-9]*$
```

Alpha strings separated by spaces (e.g. names or surnames).
```
^[a-zA-Z]+( [a-zA-Z]+)*$
```

Alphanumeric strings separated by spaces (e.g. `Route 66`).
```
^[a-zA-Z]+[a-zA-Z0-9]*( [a-zA-Z0-9]+)*$
```

Alphanumeric `unicode` strings separated by spaces (e.g. `号公路 66`).
```
^\p{L}+[\p{L}\p{N}]*( [\p{L}\p{N}]+)*$
```
 * `\p{L}` → Matches any unicode letter.
 * `\p{N}` → Matches any unicode number.
 * `[ \p{L}\p{N}]` → Allows spaces between words while ensuring each word consists of letters and numbers.

Email addresses.
```
^[^\s@]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$
```
 * `[^\s@]+` → Local part (any unicode character except spaces and @).
 * `@` → Ensures there is exactly one @ symbol.
 * `[a-zA-Z0-9.-]+` → Domain part (letters, numbers, dots and hyphens).
 * `\.` → Requires at least one dot before the TLD.
 * `[a-zA-Z]{2,}` → Ensures a valid TLD (e.g., .com, .net, .org, .ai) with at least 2 letters.

Telephone numbers.
```
^\+\d{1,4}\d{6,14}$
```
 * `\+` → Ensures the number starts with a +.
 * `\d{1,4}` → Country code (1 to 4 digits, e.g., +1, +44, +123).
 * `\d{6,14}` → Ensures the rest of the number has only digits (between 6 and 14 digits, which covers most phone numbers).

Files.
```
/^[\p{L}\p{N}_\-\s]+\.(jpg|png)$/iu
```
 * `[\p{L}\p{N}_\-\s]+` → Matches filenames that contain unicode letters, numbers, underscores, hyphens, and spaces.
 * `\.` → Matches the dot before the extension.
 * `(jpg|png)` → Ensures the filename ends with jpg or png.

## References

* [RE2](https://github.com/google/re2/wiki/Syntax)
* [MDN Regular Expression Syntax Cheatsheet](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions/Cheatsheet)
* [Regex Library](https://uibakery.io/regex-library)
