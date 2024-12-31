---
Title: Fmt
Date: 2024-09-05 17:48
tags:
  - golang
  - cheatsheet
---

| Specifier | Meaning                                         |
| --------- | ----------------------------------------------- |
| `%v`      | Default format value                            |
| `%+v`     | Value with field names (structs)                |
| `%#v`     | Go-syntax representation                        |
| `%T`      | Type of the value                               |
| `%%`      | Literal percent sign `%`                        |
| `%b`      | Binary (integers)                               |
| `%c`      | Unicode character (given an integer code point) |
| `%d`      | Decimal (integers)                              |
| `%o`      | Octal (integers)                                |
| `%x`      | Hexadecimal (lowercase)                         |
| `%X`      | Hexadecimal (uppercase)                         |
| `%e`      | Scientific notation (lowercase `e`)             |
| `%E`      | Scientific notation (uppercase `E`)             |
| `%f`      | Decimal format for floating-point               |
| `%g`      | Compact format for floating-point               |
| `%s`      | String                                          |
| `%q`      | Double-quoted string, escaped                   |
| `%x`      | Hexadecimal representation of string or bytes   |
| `%t`      | Boolean (`true` or `false`)                     |
| `%p`      | Pointer address                                 |
