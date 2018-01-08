# Tree

Tree是mac、linx下，生成文档树的一个工具，安装方式为`brew install tree`

* Listing options 

| 指令            | 作用                                       |
| ------------- | ---------------------------------------- |
| -a            | All files are listed.                    |
| -d            | List directories only.                   |
| -l            | Follow symbolic links like directories.  |
| -f            | Print the full path prefix for each file. |
| -x            | Stay on current filesystem only.         |
| -L level      | Descend only level directories deep.     |
| -R            | Rerun tree when max dir level reached.   |
| -P pattern    | List only those files that match the pattern given. |
| -I pattern    | Do not list files that match the given pattern. |
| --ignore-case | Ignore case when pattern matching.       |
| --matchdirs   | Include directory names in -P pattern matching. |
| --noreport    | Turn off file/directory count at end of tree listing. |
| --charset X   | Use charset X for terminal/HTML and indentation line output. |
| --filelimit # | Do not descend dirs with more than # files in them. |
| --timefmt <f> | Print and format time according to the format <f>. |
| -o filename   | Output to file instead of stdout.        |

* File options 

| 指令       | 作用                                       |
| -------- | ---------------------------------------- |
| -q       | Print non-printable characters as '?'.<br>无法输出的字符以？输出 |
| -N       | Print non-printable characters as is.<br>无法输出的字符保持原样|
| -Q       | Quote filenames with double quotes.      |
| -p       | Print the protections for each file.     |
| -u       | Displays file owner or UID number.       |
| -g       | Displays file group owner or GID number. |
| -s       | Print the size in bytes of each file.    |
| -h       | Print the size in a more human readable way. |
| --si     | Like -h, but use in SI units (powers of 1000). |
| -D       | Print the date of last modification or (-c) status change. |
| -F       | Appends '/', '=', '*', '@', '            |
| --inodes | Print inode number of each file.         |
| --device | Print device ID number to which each file belongs. |

* Sorting options 

| 指令          | 作用                                       |
| ----------- | ---------------------------------------- |
| -v          | Sort files alphanumerically by version.  |
| -t          | Sort files by last modification time.    |
| -c          | Sort files by last status change time.   |
| -U          | Leave files unsorted.                    |
| -r          | Reverse the order of the sort.           |
| --dirsfirst | List directories before files (-U disables). |
| --sort X    | Select sort: name,version,size,mtime,ctime. |

* Graphics options

| 指令   | 作用                                       |
| ---- | ---------------------------------------- |
| -i   | Don't print indentation lines.           |
| -A   | Print ANSI lines graphic indentation lines. |
| -S   | Print with CP437 (console) graphics indentation lines. |
| -n   | Turn colorization off always (-C overrides). |
| -C   | Turn colorization on always.             |

* XML/HTML/JSON options

| 指令          | 作用                                       |
| ----------- | ---------------------------------------- |
| -X          | Prints out an XML representation of the tree. |
| -J          | Prints out an JSON representation of the tree. |
| -H baseHREF | Prints out HTML format with baseHREF as top directory. |
| -T string   | Replace the default HTML title and H1 header with string. |
| --nolinks   | Turn off hyperlinks in HTML output.      |

* Miscellaneous options

| 指令        | 作用                                       |
| --------- | ---------------------------------------- |
| --version | Print version and exit.                  |
| --help    | Print usage and this help message and exit. |
| --        | Options processing terminator.           |