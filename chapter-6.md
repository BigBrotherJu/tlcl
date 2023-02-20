# 6. Redirection

- I/O redirection

  The “I/O” stands for input/output and with this facility we can redirect the input and output of commands to and from files, as well as connect multiple commands together into powerful command pipelines.

## Standard Input, Output, and Error

- Two kinds of output

  Many of the programs that we have used so far produce output of some kind.

  This output often consists of two types:

  - The program's results, that is, the data the program is designed to produce

  - **Status and error** messages that tell us how the program is getting along

  If we look at a command like `ls`, we can see that it displays its results and its **error** messages on the screen.

- Special files：stdout and stderr

  Keeping with the Unix theme of “everything is a file,” programs such as `ls` actually send their results to a special file called **standard output** (often expressed as **stdout**) and their status messages to another file called **standard error** (**stderr**).

  By default, both standard output and standard error are linked to the screen and not saved into a disk file.

- Special file: stdin

  In addition, many programs take input from a facility called **standard input** (**stdin**), which is, by default, attached to the keyboard.

- Change output and input

  I/O redirection allows us to change where output goes and where input comes from.

  Normally, output goes to the screen and input comes from the keyboard, but with I/O redirection, we can change that.

## Redirecting Standard Output

- Redirect stdout to file, create file if non-existent, overwrite (truncate) if existent

  - `$ ls -l /usr/bin > ls-output.txt`

    To redirect standard output to another file instead of the screen, we use the `>` redirection operator followed by the name of the file.

  - `$ > ls-output.txt` *

    Simply using the redirection operator with no command preceding it will truncate an existing file or create a new, empty file.

- Redirect stdout to file, create file if non-existent, append if existent

  `$ ls -l /usr/bin >> ls-output.txt`

  Using the `>>` operator will result in the output being appended to the file.

  If the file does not already exist, it is created just as though the `>` operator had been used.

## Redirecting Standard Error

- File stream and descriptor

  To redirect standard error we must refer to its **file descriptor**.

  A program can produce output on any of several numbered **file streams**.

  While we have referred to the first three of these file streams as standard input, output and error, the shell references them internally as file descriptors 0, 1, and 2, respectively.

- Redirect any file descriptor to a file

  The shell provides a notation for redirecting files using the file descriptor number.

  Since standard error is the same as file descriptor number 2, we can redirect standard error with this notation:

  `$ ls -l /bin/usr 2> ls-error.txt`

  The file descriptor “2” is placed immediately before the redirection operator to perform the redirection of standard error to the file `ls-error.txt`.

- `$ ls -l /bin/usr 2>> ls-error.txt`

## Redirecting Both stdout and stderr

There are two ways to do this.

- Traditional Way

  Shown here is the traditional way, which works with old versions of the shell:

  `$ ls -l /bin/usr > ls-output.txt 2>&1`

  Using this method, we perform two redirections. First we redirect standard output to the file `ls-output.txt` and then we redirect file descriptor 2 (standard error) to file descriptor 1 (standard output) using the notation `2>&1`.

- Order of the redirections

  Notice that the order of the redirections is significant.

  The redirection of standard error must always **occur after** redirecting standard output or it doesn't work.

  The following example redirects standard error to the file `ls-output.txt`: `$ ls -l /bin/usr > ls-output.txt 2>&1`.

  However, if the order is changed to the following, standard error is directed to the screen: `$ ls -l /bin/usr 2>&1 > ls-output.txt`.

- Better Way

  Recent versions of `bash` provide a second, more streamlined method for performing this combined redirection shown here:

  `$ ls -l /bin/usr &> ls-output.txt`

  We can also append the standard output and standard error streams to a single file like so:

  `$ ls -l /bin/usr &>> ls-output.txt`

## Device for Disposing of Unwanted Output

Sometimes “silence is golden,” and we don't want output from a command, we just want to throw it away.

This applies particularly to error and status messages.

- `/dev/null`

  The system provides a way to do this by redirecting output to a special file called “/dev/null”.

  This file is a system device often referred to as a **bit bucket**, which accepts input and does nothing with it.

- Throw way error messages

  To suppress error messages from a command, we do this:

  `$ ls -l /bin/usr 2> /dev/null`

## Redirecting Standard Input

### `cat`

- `$ cat ls-output.txt`

  `cat` is often used to display short text files.

  We can use it to display files without paging.

- `$ cat movie.mpeg.0* > movie.mpeg`

  Since `cat` can accept more than one file as an argument, it can also be used to **join files** together.

  Say we have downloaded a large file that has been split into multiple parts (multimedia files are often split this way on Usenet), and we want to join them back together.

  If the files were named: `movie.mpeg.001 movie.mpeg.002 ... movie.mpeg.099`, we could join them back together with this command as follows: `$ cat movie.mpeg.0* > movie.mpeg`.

  Since wildcards always expand in sorted order, the arguments will be arranged in the correct order.

- `$ cat`

  If `cat` is not given any arguments, it reads from standard input and since standard input is, by default, attached to the keyboard, it's waiting for us to type something!

  Try adding the following text and pressing Enter: `The quick brown fox jumped over the lazy dog.`

  Next, type a `Ctrl-d` to tell `cat` that it has reached end of file (EOF) on standard input.

  In the absence of filename arguments, `cat` copies standard input to standard output, so we see our line of text repeated.

- `$ cat > lazy_dog.txt` *

  We can use this behavior to create short text files.

  Let's say we wanted to create a file called `lazy_dog.txt` containing the text in our example. We would do this:

  ``` console
  [me@linuxbox ~]$ cat > lazy_dog.txt
  The quick brown fox jumped over the lazy dog.
  ```

  Type the command followed by the text we want to place in the file.

  Remember to type `Ctrl-d` at the end.

- `$ cat < lazy_dog.txt`

  Using the `<` redirection operator, we change the source of standard input from the keyboard to the file `lazy_dog.txt`.

  We see that the result is the same as passing a single filename argument.

  This is not particularly useful compared to passing a filename argument, but it serves to demonstrate using a file as a source of standard input.

## Pipelines

Using the pipe operator `|` (vertical bar), the standard output of one command can be **piped** into the standard input of another.

`command1 | command2`

- `$ ls -l /usr/bin | less`

  Remember how we said there was one we already knew that accepts standard input? It's `less`.

  We can use `less` to display, page by page, the output of any command that sends its results to standard output: `$ ls -l /usr/bin | less`

  This is extremely handy! Using this technique, we can conveniently examine the output of any command that produces standard output.

- Difference between `>` and `|`

  Simply put, the redirection operator connects a command with a file, while the pipeline operator connects the output of one command with the input of a second command.

  A lot of people will try the following when they are learning about pipelines, “just to see what happens”: `command1 > command2`.

  Here is an actual example submitted by a reader who was administering a Linux-based server appliance. As the superuser, he did this:

  ``` console
  # cd /usr/bin
  # ls > less
  ```

  The first command put him in the directory where most programs are stored and the second command told the shell to overwrite the file `less` with the output of the `ls` command. Since the `/usr/bin` directory already contained a file named `less` (the `less` program), the second command overwrote the `less` program file with the text from `ls`, thus destroying the `less` program on his system.

  The lesson here is that the redirection operator silently creates or overwrites files, so you need to treat it with a lot of respect.

- Filters

  Pipelines are often used to perform complex operations on data.

  It is possible to put several commands together into a pipeline. Frequently, the commands used this way are referred to as **filters**.

  Filters take input, change it somehow, and then output it.

### `sort`

The first one we will try is `sort`.

- `$ ls /bin /usr/bin | sort | less`

  Imagine we wanted to make a combined list of all the executable programs in `/bin` and `/usr/bin`, put them in **sorted** order and view the resulting list: `$ ls /bin /usr/bin | sort | less`.

### `uniq`

The `uniq` command is often used in conjunction with `sort`.

`uniq` accepts a sorted list of data from either standard input or a single filename argument (see the `uniq` man page for details) and, by default, removes any duplicates from the list.

- `$ ls /bin /usr/bin | sort | uniq | less`

  So, to make sure our list has no duplicates (that is, any programs of the same name that appear in both the `/bin` and `/usr/bin` directories), we will add `uniq` to our pipeline.

- `$ ls /bin /usr/bin | sort | uniq -d | less`

  If we want to see the list of duplicates instead, we add the “-d” option to `uniq`.

### `wc`

The `wc` (word count) command is used to display the number of lines, words, and bytes contained in files.

- `$ wc ls-output.txt`

  Here's an example: `$ wc ls-output.txt`.

  In this case, it prints out three numbers: lines, words, and bytes contained in `ls-output.txt`.

- `$ ls /bin /usr/bin | sort | uniq | wc -l`

  Like our previous commands, if executed without command line arguments, `wc` accepts standard input.

  The “-l” option limits its output to only report lines.

  Adding it to a pipeline is a handy way to **count things**.

  To see the number of items we have in our sorted list, we can do this: `$ ls /bin /usr/bin | sort | uniq | wc -l`。

### `grep`

`grep` is a powerful program used to find text patterns within files.

It's used like this: `grep pattern [file...]`.

- `grep` prints the lines containing patten

  When `grep` encounters a “pattern” in the file, it prints out the lines containing it.

- Patterns can be complex or simple

  The patterns that `grep` can match can be very complex, but for now we will concentrate on simple text matches.

  We'll cover the advanced patterns, called **regular expressions** in Chapter 19.

- `$ ls /bin /usr/bin | sort | uniq | grep zip`

  Let's say we wanted to find all the files in our list of programs that had the word `zip` embedded in the name. Such a search might give us an idea of some of the programs on our system that had something to do with file compression.

  We would do this: `$ ls /bin /usr/bin | sort | uniq | grep zip`.

- Options for `grep`

  There are a couple of handy options for `grep`:

  - `-i`, which causes `grep` to ignore case when performing the search (normally searches are case sensitive)

  - `-v`, which tells `grep` to print only those lines that do not match the pattern.

### `head`/`tail`

Sometimes we don't want all the output from a command. We may only want the first few lines or the last few lines.

The `head` command prints the first ten lines of a file, and the `tail` command prints the last ten lines.

- Adjust the number of printed lines

  By default, both commands print ten lines of text, but this can be adjusted with the `-n` option.

  `$ head -n 5 ls-output.txt`

  `$ tail -n 5 ls-output.txt`

- `$ ls /usr/bin | tail -n 5`

- View files in real time with `tail`

  `tail` has an option which allows us to view files in real time.

  This is useful for watching the progress of **log files** as they are being written.

  `$ tail -f /var/log/syslog`

  Using the “-f” option, `tail` continues to monitor the file, and when new lines are appended, they immediately appear on the display.

  This continues until we press `Ctrl-c`.

### `tee`

In keeping with our plumbing metaphor, Linux provides a command called `tee` which creates a “tee” fitting on our pipe.

- stdin to stdout and file

  The `tee` program reads standard input and copies it to both standard output (allowing the data to continue down the pipeline) and to one or more files.

  This is useful for capturing a pipeline's contents at an intermediate stage of processing.

- `$ ls /usr/bin | tee ls.txt | grep zip`

  Here we repeat one of our earlier examples, this time including `tee` to capture the entire directory listing to the file `ls.txt` before `grep` filters the pipeline's contents.
