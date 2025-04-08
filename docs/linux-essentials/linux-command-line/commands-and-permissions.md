# Commands and permissions

Commands syntax:

```
command option(s) argument(s)
```

## Options

Options modify the way a command works, and usually consist of a dash followed by a single letter.

Multiple options can be grouped together after a single hyphen.

## Arguments

Most commands are used with one or more arguments.

Some commands assume a default argument if none is supplied.

Arguments are optional for some commands and required by others.

## Useful commands

`whoami` to determine which user you are.

`pwd` to display your directory.

`cd` to move about directories.

`ls` to see items within working directory.

`cp` to copy a file from one directory to another.

* The third column in file info tells you the owner of the file.
* The fourth column is the group name for that file.
* Fifth column gives number of bytes for the file.
* `ll` gives same result as `ls -l`

`rm -f` to delete a file without confirming, `rm -r` to delete a directory.

`mkdir` to create a directory.

`man` with a command as argument to see man page for a command.

`date` gives the date on your system.

`more` gives output one page at a time. Piping with more is useful.

`tail` gives last line of an output. Also useful in piping.

`cat` reads contents of a file.

To become a super user (root user) use `sm -` and enter your password.

* To leave root user account: `exit`

## Permissions

`r` - read
`w` - write
`x` - execute = running a program

Each permission can be controlled at three different levels:

`u` - user
`g` - group
`o` - other = everyone on the system

To see file or directory permissions run `ls -l`:

>Example: `-rwxrwxrwx`

First bit indicates a file, next three bits are user permissions, then next three are group, and last three are permissions for others.

`chmod` can be used to change permissions.

> Example: Removing group write permissions from file `testfile`: `chmod g-w testfile`
> Example: Removing write permissions for everyone from file `testfile`: `chmod a-w testfile`

## File ownership

`chown` changes the ownership of a file.

> Example: To change the ownership from a user to root: `chown root testfile`
>
`chgrp` changes the group ownership of a file.

The `-R` option changes ownership recursively (everything within will also have ownership changed).

**Note**: If a file you do not have ownership of is within a directory that you have permissions for, you can still delete/make changes to it. For this reason is it often important to perform recursive ownership changes to ensure they are properly applied for your case.

**Source:** [Linux for Absolute Beginners: Commands and Permissions](https://alison.com/topic/learn/118892/commands-and-permissions) by Imran Afzal, Allison.