# The Unix Shell

The Shell is a program which uses command-line interface, instead of
graphical user interfaces (GUI), to run other programs rather than doing
calculations itself. The most popular Unix Shell is Bash which is
accessible by `ctrl+alt+t` keyboard shortcut in Linux computers. The
following are some great Shell tutorials:

- [The Unix Shell](http://swcarpentry.github.io/shell-novice/)
- [Extra Unix Shell
  Material](http://swcarpentry.github.io/shell-extras/)
- [Introduction to using the shell in a High-Performance Computing
  context](https://hpc-carpentry.github.io/hpc-shell/)

This tutorial provides a reference of some practical commands in the
Unix Shell and important text editors in Bash.

------------------------------------------------------------------------

## Tab completion

In the Unix Shell we can use **tab completion** to type commands faster
and easier. To do that press `tab` after typing the beginning of your
command and let Bash complete the command. If there are more than one
function or directory corresponded to the beginning that you typed, Bash
will not return anything if your press `tab` once. In this case, if you
press `tab` for the second time Bash will show all the options.

## Wildcards

A string is a wildcard pattern if it contains one of the characters `?`,
`*` or `[`. Globbing is the operation that expands a wildcard pattern
into the list of pathnames matching the pattern. For more information on
globbing pathnames typing `man 7 glob`.

**Matching:**

- A `?` matches any single character. For example, `hd?` would look for
  `hda`, `hdb`, `hdc` and every other letter/number between `a-z`, `0-9`
- A `*` matches any string, including the empty string. For example,
  `hd*` would look for `hd`, `hdf`, `hd-full`, and anything that starts
  with `hd` also including `hd` itself. And `m*l` could by `mail`,
  `mall`, `ml`, and anything that starts with an `m` and ends with an
  `l`

**Character classes:**

- An expression `[  ]`, where the first character after the leading `[`
  is not an `!`, matches any of the characters enclosed by the brackets.
  For example, `m[a-d]m` can become anything that starts and ends with
  `m` and has any character `a` to `d` in between.
- An expression `[! ]`, where the first character after the leading `[`
  is an `!`, matches any character that is not enclosed by the brackets.

## Shell Expansions

- Brace expansion: is a mechanism by which arbitrary strings may be
  generated for example `echo 1{2,3}4` returns 124 and 134 or
  `echo {1..3}` returns 1,2, and 3
- Command substitution: it allows the output of a command to replace the
  command itself for example, `echo $(date)` returns the actual date.
  Note that for the environmental variables you cannot use `()`, for
  example `echo $HOME` or `echo ${HOME}` is the correct way

## Basic commands

The following is a list of basic Bash commands. You may find a short
explanation next to each command.

``` bash
man <command> # user manual of the command (enter q to exit)
<command> --help # display brief help
uname # print operating system name
alias # show alias 
env # show all environmental variables
w # show current users
hostnme # show the host nsme
whoami # show the user name
id # shows your id
passwd # change user password
nproc # show number of processors
lscpu # list CPU, display information about the CPU architecture
free -h # show amount of memory RAM 
ps # report a snapshot of the current processes
file # determine file type
date # show date and time 
pwd # print working directory
cd # change directory. Use cd .. or ~ or / to go back or home or system dir
ls # lists. Use flages -al to see all files in long formats
cp # copy a file. Use -r to copy a directory recursively 
scp # secure copy a file. Use -r to copy a directory 
sftp # secure file transfer program (SSH file transfer protocol)
wget # the non-interactive network downloader (-O <newname> to rename)
curl # copy a url. Use -o to name the output 
md5sum # compute MD5 message digest. Use -c to check the digits
tar -c/xzf # to archive and create(c)/extract(x) a compressed(z) file(f)
ln # make links between files
mv # move
rm # remove file. Use -r to remove a directory
mkdir # make a directory
rmdir # remove an empty directory
install -dvp # make a directory(d), verbose(v) and parent(p)
cat # concatenate files and print on the standard output
zcat # concatenate compressed (zip) files
diff <file1> <file2> # compare files line by line. Use -y for side by side and -q for report only when files differ
less # to view the contents of a text file one screen at a time (less than a text editor)
touch # generate a new file that contains no data
chmod # change file mode for user(u), group(g) or other(o) to give(+) or take(-) permission for read(r), write(w), or execute(x) (example chmod u+r)
echo # display a line of text ex. echo === $(date)
cut -f <field number> -d <delimiter> # cut field number based on the delimiter
grep # print lines matching a pattern (global regular expression print)
sed # stream editor for filtering and transforming text
tr # translate or delete characters (for example 'tr -d ,' removes comma)
awk # pattern scanning and text processing language
wc # word count; it counts the number of lines(-l), words(-w), and characters(-m) of files 
nl # number lines of files
head -n <number> # output the n first lines of files
tail -n <number> # output the n last lines of files
sort # sort lines of text files (use flag -r for reverse). Use -n to sort numerically
uniq # remove adjacent duplicated lines from input. Use -c to see number of times the line occurred 
find <dir> -name file_name # search for files in a directory hierarchy by name. Use -iname for case insensitive search
which # locate a program file in the user's path
history # show history of commnads
!<number> # rerun the command with the number from history
!! # rerun the last command (bang bang)
bc # Bash calculator language ex. echo '3 + 4' | bc
clear (ctrl+l) # clear terminal
exit (ctrl+d) # to exit
```

For practice, let’s create two text files including some names and
grades by `cat` command in `bash_test` directory:

``` bash
mkdir bash_test
cd bash_text

cat > names.txt
Dori
Ari
Ashi
Jackie
Dori
# press `ctrl+d` to exit

cat > grade.txt
A
B+
A-
A
B
# press `ctrl+d` to exit

ls
```

`ls` command returns `grade.txt  names.txt` that shows we already made
the files. Now, let’s see head, tail and number of lines in both files:

``` bash
head -n 3 n*.txt
echo ---
tail -n 3 g*.txt
echo ---
wc -l [n,g]*.txt

## Dori
## Ari
## Ashi
## ---
## A-
## A
## B
## ---
##  5 grade.txt
##  5 names.txt
## 10 total
```

For finding things we can use `grep` or “global/regular
expression/print” command. For example, let’s find lines that contain
the letter “D”:

``` bash
grep D names.txt

## Dori
## Dori
```

There are several options that we can use for `grep` command. For
example, `grep -w` is searching for the exact word, `-n` option shows
numbers the lines that match, `-i` flag makes our search
case-insensitive, or `-v` inverts our search to the lines that do not
contain the pattern, or `-o` print only the matched parts, and `-P` flag
for using Perl-compatible [regular
expression](https://docs.python.org/3/library/re.html#re-syntax). To see
all the option use `man grep`. Lets’ try to find lines which do not
contain letter “d” or “D”:

``` bash
grep -inv d names.txt

## 2:Ari
## 3:Ashi
## 4:Jackie
```

While `grep` finds lines in files, the `find` command finds files
themselves. For instance, in directory `bash_test` command `find .` will
shows all files and directories within the current directory. The
following command will return number of lines in `names.txt` and
`grade.txt` files in the directory:

``` bash
wc -l $(find . -name '[n,g]*.txt')

##  5 ./grade.txt
##  5 ./names.txt
## 10 total
```

For another example, you may use the command in below to print a
divider, like `===`, followed by date and hostname:

``` bash
echo === $(hostname) $(date)
# Or
echo === $(hostname) "date: $(date)"
```

## Pipes and Filters

Now that we know a few basic commands, we can combine the programs and
commands in new ways. The following commands let us to use output of a
command as an input for another command or store the outputs of commands
in a separate file.

``` bash
first | second # is a pipeline; the output of the first command is used as the input to the second 
command > file # redirects a command’s output to a file (overwriting any existing content)
command >> file # appends a command’s output to a file
< # operator redirects input to a command
```

For example let’s remove the duplicated names in the `names.txt`:

``` bash
sort names.txt | uniq 
echo --- To count number of occurrences ---
sort names.txt | uniq -c

## Ari
## Ashi
## Dori
## Jackie
## --- To count number of occurrences ---
##       1 Ari
##       1 Ashi
##       2 Dori
##       1 Jackie
```

Or make a new file, `count.txt`, including number of lines, words, and
characters in the text files:

``` bash
wc [n,g]*.txt > count.txt
```

Use `cat count.txt` to see the file content. Also, you may use:

``` bash
cat count.txt
wc -l < count.txt

##  5  5 12 grade.txt
##  5  5 26 names.txt
## 10 10 38 total
## 3
```

To find number of lines in the `count.txt`. Note that you also can use
`wc -l count.txt` to find the number of lines.

## Loops and conditional constructs

Loops are key to productivity improvements through automation as they
allow us to execute commands repeatedly. Similar to wildcards and tab
completion, using loops also reduces the amount of typing and mistakes.
The syntax is:

``` bash
for variable in file1 file2 ...; do command_1 $variable; command_2; ...; done
# Or
for output in $(command);  do command_1 $output; command_2; ...; done
```

For instance, let’s make a copy of `grade.txt` and `names.txt`:

``` bash
for x in [g,n]*.txt; do cp $x copy-$x; echo copy-$x; done

## copy-grade.txt
## copy-names.txt
```

Use `ls` to see new files that start with `copy-` in your directory.
Another example,

``` bash
for y in $(seq 1 3); do echo "The number is $y"; done
echo --- Same as ---
for y in {1..3}; do echo "The number is $y"; done

## The number is 1
## The number is 2
## The number is 3
## --- Same as ---
## The number is 1
## The number is 2
## The number is 3
```

Conditional statements help us to write an `if` construction. In general
we can write the test statement by `[ Expression ]`. The syntax is:

``` bash
if [ Expression ]; then command; elif [ Expression ]; then command; ...; else command; fi
```

For example, let’s print “File exist” if `count.txt` is exist (note that
there is a space after `[` and before `]`):

``` bash
if [ -e count.txt ]; then echo "File exist"; else echo "File does not exist"; fi
echo --- Or ---
if [ ! -e count.txt ]; then echo "File does not exist"; else echo "File exist"; fi
echo --- Or ---
if [ ! -e count.txt ]; then echo "File does not exist"; elif [ -e count.txt ]; then  echo "File exist"; else echo "NA"; fi

## File exist
## --- Or ---
## File exist
## --- Or ---
## File exist
```

To see all the test expressions see `man test`.

## Text editors

Most popular text editors in Bash:

- Vi
- Nano
- Emacs

To open the text editors simply run `vi`, `nano` or `emacs -nw`. You may
use `ctrl+z` to suspend the editor and return to the Bash terminal and
enter `fg` in the Bash terminal to return the editor. To exit, in Vi
first press `esc` and then enter `:q!`, in Nano you may use `ctrl+x`,
and in Emacs `ctrl+x ctrl+c`. Vi and Emacs have more futures in
comparison to Nano but they are more difficult as well.

The following are some important commands in Nano. Note that `^` is
`ctrl` and `M-` is `alt`.

- `^s`: save
- `^o`: write out (save with a new name)
- `^x`: exit
- `^z`: suspend nano (if activated)
- `^k`: cut the line
- `M-6`: copy the line
- `^u`: uncut/paste the line
- `^w`: where is (search)
- `^\`: search and replace
- `M-g`: go to line
- `M-a`: select text
- `M-u`: undo
- `M-e`: redo
- `^t`: spelling check (need to install `spell` package)
- `^j`: justify text
- `^g`: help (`F2`)

The following are some important commands in Emacs. Note that `C-` is
`ctrl` and `M-` is `alt`.

- `C-x C-c`: exit
- `C-z`: suspend
- `C-k`: kill the line
- `C-w`: cut the line/text
- `M-w`: copy the line/text
- `C-y`: uncut/paste the line/text (yank)
- `C-space arrow keys`: select text
- `C-shift arrow keys`: select paragraphs
- `C-x u`: undo
- `C-a`: move to the beginning of the line
- `C-e`: move to the end of the line
- `C-home`: move to the beginning of the buffer
- `C-end`: move to the end of the buffer
- `M-g g`: go to line
- `C-s`/`C-r`: search
- `M-%`: replace (`y` yes, `n` no, `!` all)
- `C-g`: stop a command
- `C-x C-f`: make/open a file as a new buffer
- `C-x b`: change the buffer
- `C-x k`: kill the buffer
- `C-x 1`: close other windows
- `C-x 0`/`q`: close/quit windows
- `C-x o`: switch to other windows
- `C-h ?`: help list
- `C-h t`: tutorial
- `C-h d`: search help for a pattern
- `C-h c`: show help for the command
- `M-x <command>`: run commands
- `M-x ispell`: spell check; enter the suggested `digit` or `a` to
  accept or `r` to rewrite
- `M-x package-install`: install packages
- `M-x package-list-packages`: list of packages

You may find more about Emacs in [here](emacs.html).

## Shell script

Now, we can make Shell script to crate a small program including Bash
commands and other programs that we want. Let’s make a program to shows
rows 3 to 5 of a file in Shell scripts. Use `nano script.sh` to open
`nano` text editor to make `script.sh` and insert the following lines:

``` bash
#!/bin/bash
sort names.txt | head -n 5 | tail -n 3
```

The first line shows the language of the program which is Bash in here.
To run the program use: `{bash}  bash script.sh`

You may use the following program to show rows 3 to 5 of a given file.
Use `nano script_1.sh` and insert the following lines:

``` bash
#!/bin/bash
sort "$1" | head -n 5 | tail -n 3
```

To run the code use:

``` bash
bash script_1.sh names.txt

## Dori
## Dori
## Jackie
```

Also we can write a program that works for any given files. Use
`nano script_all.sh` and insert the following lines:

``` bash
#!/bin/bash
for line in "$@"; do sort $line | head -n 5 | tail -n 3; done
```

To run the code use:

``` bash
bash script_all.sh names.txt grade.txt

## Dori
## Dori
## Jackie
## A-
## B
## B+
```

For another example let write a program to find a certain pattern within
some files in `bash_test` directory. Use `nano name_select.sh` and
insert:

``` bash
#!/bin/bash
grep -w $1 -r $2 | cut -d : -f 2 > $1.txt
```

To find name `Dori` among all files in the current directory (`.`) use:

``` bash
bash name_select.sh Dori .
```

To see the output run `cat Dori.txt`.

---

Copyright, [Ashkan Mirzaee](https://ashki23.github.io/index.html) | Content is available under [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) | Sourcecode licensed under [GPL-3.0](https://www.gnu.org/licenses/gpl-3.0.en.html)
