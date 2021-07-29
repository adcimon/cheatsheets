# Regular Expressions

[Regular expressions](https://en.wikipedia.org/wiki/Regular_expression) are a particular kind of formal grammar used to parse strings and other textual information that are known as Regular Languages in formal language theory.

| Symbols | |
| - | - |
| `^` | Start of the string. |
| `$` | End of the string. |

| Characters | |
| - | - |
| `\d` | Digit. |
| `\w` | Word. |
| `\s` | Whitespace, tab and line break characters. |
| `.` | Any character. |

| Composites | |
| - | - |
| `xy` | `x` followed by `y`. |
| `x\|y` | `x` or `y` (prefer `x`). |

| Repetitions | |
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

## Examples

Begins with "The".
```
^The
```

Ends with "end".
```
end$
```
