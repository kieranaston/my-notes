# Help commands and pipes

## Help commands

3 types of help commands:

* `whatis command`
  * Gives shorter version of command info
* `command --help`
  * Longer version of help for command
* `man command`
  * Full info for command

## Tab and up arrow

Tab completes available commands, files, or directories.

Up arrow gives the last executed command.

## Pipes

Pipes are used to connect the output of one command to the input of another command.

The symbol for a pipe is `|`. Syntax for using pipes is:

```
command1 [arguments] | command2 [arguments]
```

## Adding text to files

3 simple ways:

* `vi` editor
* Redirect command output `>` or `>>`
* `echo >` or `>>`

**Example using redirect**: `echo "Jerry is the main character in Seinfeld" > jerry` populates file `jerry` with that text.

Doing it with `>` will overwrite contents. `>>` will add to the existing contents.

Can also send the output of a command to a file this way.

**Source:** [Linux for Absolute Beginners: Help Command and Pipes](https://alison.com/topic/learn/118893/help-command-and-pipes) by Imran Afzal, Allison.