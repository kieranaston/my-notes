# File comparison and splitting

## Cut command

Cut is a command utility that allows you to cut parts of lines from specific files or piped data and print the result to standard output.

Can be used to cut parts1 of a line by a delimiter, byte position, and character.

`cat -c1 filename` list one character
`cut -c1,2,4` pick and choose character(s)
`cut -c1-3 filename` list range of characters
`cut -c1-3, 6-8 filename` list by specific range of characters
`cut -b1-3 filename` list by byte size
`cut -d: -f 6 /etc/passwd` list first 6th column separated by :
`cut -d: -f 6-7 /etc/passwd` list first 6 and 7th column separated by :
`ls -l | cut -c2-4` only print user permissions of files/dir

## Compare files

`diff` compares line by line
`cmp` compares byte by byte

## Comtining and plitting files

Multiple files can be combined into one, and one file can be split into multiple files.

In times when we have huge files, there are times when we need to either split them or compress them to send them places.

`split -l 2 countries sep` splits the file countries into files with name `sep` containing 2 lines each from original countries file

## Linux vs. Windows commands

Listing of a directory: `dir` vs `ls -l`
Rename a file: `ren` vs `mv`
Copy a file: `copy` vs `cp`
Move file: `move` vs `mv`
Clear screen: `cls` vs `clear`
Delete file: `del` vs `rm`
Compare contents of files: `fc` vs `diff`
Search for a word/string in a file: `find` vs `grep`
Display command help: `command /?` vs `man command`
Displays your location in the file system: `chdir` vs `pwd`
Displays the time: `time` vs `date`

**Source:** [Linux for Absolute Beginners: File Comparison and Splitting](https://alison.com/topic/learn/118896/file-comparison-and-splitting) by Imran Afzal, Allison.