# Regular Expressions

[Regular expressions](https://en.wikipedia.org/wiki/Regular_expression) are a particular kind of formal grammar used to parse strings and other textual information that are known as Regular Languages in formal language theory.

| Symbols | |
| - | - |
| `^` | Start of the string. |
| `$` | End of the string. |

| Composites | |
| - | - |
| `xy` | `x` followed by `y`. |
| `x|y` | `x` or `y` (prefer `x`). |

| Repetitions | |
| - | - |
| `?` | 0 or 1 occurrences. |
| `+` | At least 1 occurrence. |
| `*` | Any number of occurrences. |

## Examples

Begins with "The".
```
^The
```

Ends with "end".
```
end$
```
