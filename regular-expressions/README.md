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
| `a-z` | Character in range `a-z`. |
| `A-Z` | Character in range `A-Z`. |
| `0-9` | Digit in range `0-9`. |

| Flags | |
| - | - |
| `/x/g` | Global, find all matches rather than stopping after the first match. |
| `/x/m` | Multi line, `^` and `$` match the start and end of a line. |
| `/x/i` | Case insensitive. |

Characters `^.[$()|*+?` can be used with a backslash `\`.

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
^(^$)|(<OTHER_REGEXP>)$
```

Alphanumeric string (e.g. nicknames).
```
^[a-zA-Z]+[a-zA-Z0-9]*$
```

Alpha strings separated by spaces (e.g. names or surnames).
```
^[a-zA-Z]+( [a-zA-Z]+)*$
```

Alphanumeric strings separated by spaces (e.g `Route 66`).
```
^[a-zA-Z]+[a-zA-Z0-9]*( [a-zA-Z0-9]+)*$
```

## References

* [RE2](https://github.com/google/re2/wiki/Syntax)
* [MDN Regular Expression Syntax Cheatsheet](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions/Cheatsheet)
* [Regex Library](https://uibakery.io/regex-library)
