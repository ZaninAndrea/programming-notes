# Chapter 7
<!-- toc -->

## Command line mode options
Most input lines entered at the shell prompt have three basic elements: command, options, arguments. E.g. `command argument1 argument2 --option`

If `sudo` is not configured follow [this](https://courses.edx.org/courses/course-v1:LinuxFoundationX+LFS101x+1T2017/courseware/fef2ac9b822744958447641cbe43212c/a025f50546dd4b1894c6c9a72dfb654b/)

Virtual Terminals (VT) are console sessions that use the entire display and keyboard outside of a graphical environment.
To switch between the VTs, press `CTRL-ALT-corresponding function key` for the VT. For example, press `CTRL-ALT-F6` for VT 6

## Basic operations
![](/assets/k086v9ac.bmp)
The `halt` and `poweroff` commands issue `shutdown -h` to halt the system

The command `which` locates a program in your filesystem (e.g. `which diff`), if it doesn't find the program try `whereis`, which  looks for it in a broader range of directories.

Navigation commands:
* `pwd` Displays the present working directory
* `cd <directory>` navigates to the specified directory
* `ls` lists the content of the current directory
    * `ls -a` includes hidden files
* `tree` displays a treeview of the filesystem
    * `tree -d <directory>` displays a treeview of the content of the specified directory

Relative paths: `.` (present directory), `..` (parent directory) and `~` (ALT+126) (your home directory).

Links:
* `ln file1 file2` command creates **hard links**, which means having a single file with multiple names. The inode for both will be the same.
* `ln file1 file2 -s` creates **soft links**, aka symbolic links. Those are not files , but point to files. You can think of them as shortcuts.

## Working with files
Basic utilities:
* `cat`: prints out a file or combine files
* `head` show the first few lines of a file
* `tail`: shows the last few lines of a file
* `less`: a paging program, shows the file and has you can Use `/` to search for a pattern in the forward direction and `?` for a pattern in the backward direction
* `man`: shows documentation
* `touch <filename>` creates an empty file
    * `touch -t <time> <filename>` changes the timestamp to a specific time
* `mkdir <dirname>` creates a new directory
* `mv <oldname> <newname>` to move or rename a file or directory
* `rm <name>` to remove the file or directory, use `-f` flag to remove forcefully, `-i` to remove interactively, use `-rf` to remove recursively all the directory's content

The **PS1** variable is the character string that is displayed as the prompt on the command line. For example to create a prompt like this `student@quad32 $` you can set PS1 to `\u#\h \$` using `PS1="\u@\h \$ "` 

## Searching for files
* `locate <string>` performs a search through a previously constructed database of files and directories on your system, matching all entries that contain the string
* `ls <query>` the query can contain wildcards (see below). The command will search only in the current directory
* `find <directory>` Searches files in the given directory (or when no argument are passed the current) and all subdirectories. 
    * `-name <name>` flag shows only files with a certain name
    * `-type d` or `-type f` to only show files or directories
    * `-exec <command>` executes a command on the files matching the criteria, you can use the placeholder `{}` that will be filled with the matching file's name. You must end the command with "\;" or ‘;’ (including quotes). E.g. `find -name "*.swp" -exec rm {} ’;’` to remove all files that end with .swp
    * `-ctime <days>` only shows files which inode metadata was changed less than `<days>` days ago. Days can also be exact numbers (n), +n or -n
    * `-atime <days>` as ctime, but with last read
    * `-mtime <days>` as ctime, but with last modified
    * `-size <size>` Note the size here is in 512-byte blocks, by default; you can also specify bytes (c), kilobytes (k), megabytes (M), gigabytes (G), etc. File sizes can also be exact numbers (n), +n or -n. For example, to find files greater than 10 MB in size and running a command on those files: `find / -size +10M -exec command {} ’;’`

Wildcards:

| Wildcard | Result |
|---|---|
| ? | Matches any single character |
| * | Matches any string of characters |
| [set] | Matches any character in the set of characters, for example [adf] will match any occurrence of "a", "d", or "f" |
| [!set] | Matches any character not in the set of characters |

When commands are executed, by default there are three standard file streams (or descriptors) always open for use: **standard input** (standard in or **stdin**), **standard output** (standard out or **stdout**) and **standard error** (or **stderr**).

Usually, stdin is your keyboard, stdout and stderr are printed on your terminal

In Linux, all open files are represented internally by what are called file descriptors. Simply put, these are represented by numbers starting at zero. stdin is file descriptor 0, stdout is file descriptor 1, and stderr is file descriptor 2

Redirecting the streams:
* `do_something < input-file` to change the input source to a file. You can prepend the `<` the file descriptor number if you want to redirect a different stream. E.g. `do_something 2> error-file`
* `do_something > output-file` to change the output source to a file
* `command1 | command2` to **pipe** the output of command1 as input of command2, this can be concatenated in a **pipeline**, e.g. `command1 | command2 | command3`
* 

