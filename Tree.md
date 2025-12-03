---
Title: Tree
Date: 29.07.2023
Time: 21:20
Tags: [cheatsheet]
---

## Deprecated / LTS instead

### Count files in folder

```bash
tree -a -f <directory_path> | grep -c -P '\/[^\/]+$'
```


## CheatSheet

| command                                   | **description**                                                            |
| ----------------------------------------- | -------------------------------------------------------------------------- |
| tree -L \<depth\>                         | **Display the directory tree for the current directory (recursive)**       |
| tree /path/to/directory                   | **Display the directory tree for a specific directory (non-recursive)**    |
| tree -L \<depth\> /path/to/directory      | **Display the directory tree for a specific directory (recursive)**        |
| tree -h                                   | **Display the directory tree with file sizes in human-readable format**    |
| tree -a                                   | **Display the directory tree with hidden files and directories**           |
| tree -q                                   | **Display the directory tree without including the "ASCII line graphics"** |
| tree -d                                   | **Display the directory tree, only showing directories**                   |
| tree > output.txt                         | **Save the directory tree to a file**                                      |
| tree -\I "\<directory1\>\|\<directory2\>" | **Exclude specific directories from the tree**                             |
|                                           |                                                                            |

