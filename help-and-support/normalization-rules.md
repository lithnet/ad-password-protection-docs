# Normalization Rules

The password filter provides the option of using a normalization technique, that when enabled, allow you to prevent the use of common character substitutions and patterns that can lead to easily guessable passwords.

If you take the example `P@ssw0rd` - a simple variant of the word `password` with some well-known substitutions. While the symbol, number, and uppercase letter are enough to keep most complexity filters happy, these well-known substitutions provide no additional difficulty to modern password cracking tools. Users will commonly make predictable modifications to dictionary words such as the common `Winter2018`. Adding `winter` to the banned store prevents the use of `Winter2018`, `Winter2019` and all other variants into the future.

The normalization process applied to the string is as follows

1. Lower case the string according to the invariant culture rules
2. Remove all whitespace from the string
3. Remove the following leading and trailing symbols and numbers from the string

```
0123456789!@#$%^&*(){}[];:"'<>,.?\/+_=-~`
```

1. Substitute the following characters found in the string

| character | substitution |
| --------- | ------------ |
| \_        |              |
| .         |              |
| +         |              |
| $         | s            |
| 0         | o            |
| 4         | a            |
| 3         | e            |
| @         | a            |
| ^         | a            |
| (         | c            |
| 6         | g            |
| 1         | i            |
| 7         | t            |
| 8         | b            |
| 2         | z            |
| !         | i            |

### Examples

The following table highlights some normalization results on common patterns

| Input        | Normalized output |
| ------------ | ----------------- |
| P@55w0rd!123 | password          |
| Winter2017!  | winter            |
| Lithnet123!  | lithnet           |
| r3qu1r3m3nt5 | requirements      |
