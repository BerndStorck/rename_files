# repsign 1.3.0

repsign replaces one single character or a text string with another character or text string in the names of all files in a given directory. By default, it will replace all blanks in the file names with an underscore in the names of all files in the current working directory.

## 1. Calls

1. `repsign`
2. `repsign <one_character>`
3. `repsign <one_string> <another_string>`
4. `repsign <path> <one_string> <another_string>`
5. `repsign -t|--tr|--translate <one_string> <another_string>`
6. `repsign <path> -t|--tr|--translate <one_string> <another_string>`
7. `repsign -h|--help`

### 1.1. Explanation of Calls

1. By default, the program replaces all blanks with an underscore in all file names in the current directory. 
2. If repsign is called with exactly one parameter, one single 
   character, it will replace that character with an underscore. 
3. With two parameters you can decide, which string should be replaced 
   with which other text string. 
   - `repsign '?' _`  would replace any question mark in the file names by an underscore.
   - `repsign '*' -` would replace any asterisk in file names by a minus.
4. If you are using three parameters, then the first is the directory, 
   in which should be changed, the second says, which string should 
   be replaced, and the third says, which other string should be 
   inserted instead. Such a call can look like the following:
   
   - `repsign /home/rudolf/downloads "ü" "ue"`
   
   This example shows that repsign expects the path specification without a concluding slash, and also demonstrates that repsign can replace one character by several.

#### Translate Modus

5. If the first of three parameters is `-t`, `-tr` or `--translate` then each character from the second parameter is replaced by the corresponding character from the third parameter.
6. If there are four call parameters, the first means the directory in which file names are to be changed, the second must be the option  `-t`, `-tr` or `--translate`. The program will then replace each character from the third
       parameter with the corresponding character from the fourth parameter.

### 1.2. Special Replacements

You can replace questions marks "?" in file names for example by:

```shell
repsign '?' _
```

You can replace asterisks "*" in file names for example by:

```shell
repsign '*' -
```
