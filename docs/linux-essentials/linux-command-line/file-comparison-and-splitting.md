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

**Source:** [Linux for Absolute Beginners: File Comparison and Splitting](https://alison.com/topic/learn/118896/file-comparison-and-splitting) by Imran Afzal, Allison.