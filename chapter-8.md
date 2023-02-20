# 8. Advanced Keyboard Tricks

## Command Line Editing

- Readline

### Cursor Movement

- `Ctrl-l`

  Clear the screen and move the cursor to the top-left corner.

  The `$ clear -x` command does the same thing.

- `$ clear` clears scrollback buffer

### Modifying Text

### Cutting and Pasting Text

- Killing and yanking

  The Readline documentation uses the terms **killing and yanking** to refer to what we would commonly call cutting and pasting.

- Kill-ring

  Items that are cut are stored in a buffer (a temporary storage area in memory) called the **kill-ring**.

### Meta Key

Since the developers of Readline could not be sure of the presence of a dedicated extra control key, they invented one and called it **meta**.

On modern keyboards this maps to the `Alt` key but it wasn't always so.

While the `Alt` key serves as the meta key on modern keyboards, you can also press and release the `Esc` key to get the same effect as holding down the `Alt` key if you're still using a terminal (which you can still do in Linux!).

## Completion

- Press `Tab` once to complete

- Types of completion

  While this example shows completion of **pathnames**, which is its most common use, completion will also work on:

  - variables (if the beginning of the word is a `$`),

  - user names (if the word begins with `~`),

  - commands (if the word is the first word on the line)

  - and hostnames (if the beginning of the word is `@`).

    Hostname completion works only for hostnames listed in `/etc/hosts`.

- Completion commands

  There quite a few more that are rather obscure.

  - `Alt-?`

    Display a list of possible completions.

    On most systems you can also do this by pressing the `Tab` key a **second** time, which is much easier.

  - `Alt-*`

    Insert all possible completions. This is useful when you want to use more than one possible match.

- Programmable completion

  Recent versions of `bash` have a facility called **programmable completion**.

  Programmable completion allows you (or more likely, your distribution provider) to add additional completion rules.

  Usually this is done to add support for specific applications. For example, it is possible to add completions for the **option list** of a command or match particular file types that an application supports.

  Ubuntu has a fairly large set defined by default.

  Programmable completion is implemented by **shell functions**, a kind of mini shell script that we will cover in later chapters.

  If you are curious, try the following: `$ set | less`, and see if you can find them.

  Not all distributions include them by default.

## Using History

This list of commands is kept in our home directory in a file called `.bash_history`.

### Searching History

- `$ history | less`

  At any time, we can view the contents of the **history list** by doing the following: `$ history | less`.

- Number of command history

  By default, `bash` stores the last 500 commands we have entered, though most modern distributions set this value to 1000.

  We will see how to adjust this value in Chapter 11.

- `$ history | grep /usr/bin`

  Let's say we want to find the commands we used to list `/usr/bin`.

  This is one way we could do this: `$ history | grep /usr/bin`.

  And let's say that among our results we got a line containing an interesting command like this:

  ``` console
   88  ls -l /usr/bin > ls-output.txt
  ```

  The `88` is the line number of the command in the history list.

- History expansion

  We could use this immediately using another type of expansion called **history expansion**.

  To use our discovered line, we could do this: `$ !88`.

  `bash` will expand `!88` into the contents of the 88th line in the history list.

  There are other forms of history expansion that we will cover in the next section.

- Search history incrementally (see bash doc for more info)

  `bash` also provides the ability to search the history list incrementally.

  This means we can tell `bash` to search the history list as we enter characters, with each additional character further refining our search.

  To start incremental search press `Ctrl-r` followed by the text we are looking for.

  When we find it, we can either press `Enter` to execute the command or press `Ctrl-j` to copy the line from the history list to the current command line.

  To find the next occurrence of the text (moving “up” the history list), press `Ctrl-r` again.

  To quit searching, press either `Ctrl-g` or `Ctrl-c`.

- History commands

### History Expansion

### `script`

In addition to the command history feature in `bash`, most Linux distributions include a program called `script` that can be used to record an entire shell session and store it in a file.

The basic syntax of the command is as follows: `script [file]`, where file is the name of the file used for storing the recording.

If no file is specified, the file `typescript` is used.

See the `script` man page for a complete list of the program’s options and features.
