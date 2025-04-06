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