# Text and grep commands

## Filters/text processors commands

* `cut` cut output of command
* `awk` list by the columns
* `grep` and `egrep` search by keywords
* `sort` sorts output
* `uniq` no duplicates in output
* `wc` word count

>Example of `grep`: To search for directories with user read and write permissions: `ls -l | grep drw`

## `grep` usage

`grep keyword file` gives only the lines of `file` that contain `keyword`
`grep -c keyword file` this searches for a keyword and counts it
`grep -i KEYword file` searches for keyword but ignore case
`grep -n keyword file` displays the matched lines and line numbers
`grep -v keyword file` get everything **but** the search keyword
`grep keyword file | awk '(print $1)'` gives only first columns of the lines returned
`ls -l | grep Desktop` only pull results that include "Desktop"
`egrep -i "keyword|keyword2" file` gives all lines matching either of the keywordsx

## `wc` usage

Reads either standard input or list of files and generates: newline count, word count, byte count.

`wc file` checks file line count, word count, byte count
`wc -l file` gets number of lines in a file
`wc -w file` gets number of words in a file
`wc -b file` gets number of bytes in a file

`ls -l | wc -l` gives the number of files/directories you have within a location (plus 1 extra line counted)

## `awk` usage

Most of the time `awk` is used to extract fields from a file or from an output.

**Source:** [Linux for Absolute Beginners: Text and Grep Commands](https://alison.com/topic/learn/118895/text-and-grep-commands) by Imran Afzal, Allison.