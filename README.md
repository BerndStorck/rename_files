# repsign 1.2.0

repsign replaces one single character or a text string with another character or text string in the names of all files in a given directory. By default, it will replace all quotation marks in the file names with an underscore in the names of all files in the current working directory.

## Calls

1. `repsign`
2. `repsign <one_character>`
3. `repsign <one_string> <another_string>`
4. `repsign <path> <one_string> <another_string>`
5. `repsign -h|--help`

### Explanation of Calls

**Call the programm with `repsign --help` to get more information.**

### Special Replacements

You can replace questions marks "?" in file names for example by:

```shell
`repsign '?' _`
```

You can replace asterisks "*" in file names for example by:

```shell
`repsign '*' -`
```
