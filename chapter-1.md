# 1. What Is the Shell?

## Terminal Emulators

## Terminal Sessions

## Shell Prompt

``` console
[me@linuxbox ~]$
```

This is called a **shell prompt** and it will appear whenever the shell is ready to accept input.

- `$`

- `#`

  If the last character of the prompt is a pound sign (“#”) rather than a dollar sign, the **terminal session** has **superuser privileges**.

  This means either we are logged in as the **root user** or we selected a terminal emulator that provides **superuser (administrative) privileges**.

## Command History

- `up-arrow` and `down-arrow`

  Press `up-arrow` and `down-arrow` to see **command history**.

  Most Linux distributions remember the last 1000 commands by default.

## Cursor Movement

- `left-arrow` and `right-arrow`

## X Window System

The X Window System is the underlying engine that makes the GUI go.

- Quick copy and paste technique

  A mechanism built into the X Window System supports a quick copy and paste technique.

  If you **highlight some text** by holding down the left mouse button and dragging the mouse over it (or double clicking on a word), it is copied into a buffer maintained by X.

  **Pressing the middle mouse button** will cause the text to be pasted at the cursor location.

- Conventional copy and paste doesn't work

  Don't be tempted to use `Ctrl-c` and `Ctrl-v` to perform copy and paste inside a terminal window. They don't work.

  These control codes have different meanings to the shell and were assigned many years before the release of Microsoft Windows.

- Focus policy

  Your graphical desktop environment (most likely KDE or GNOME), in an effort to behave like Windows, probably has its **focus policy** set to “click to focus.”

  This means for a window to get focus (become active) you need to click on it.

  This is contrary to the traditional X behavior of “focus follows mouse” which means that a window gets focus just by passing the mouse over it.

  The window will not come to the foreground until you click on it but it will be able to receive input.

  Setting the focus policy to “focus follows mouse” will make the copy and paste technique even more useful.

## Ending a Terminal Session

We can end a terminal session:

- by either closing the terminal emulator window,
- by entering the `exit` command at the shell prompt,
- or pressing `Ctrl-d`.

## Special Terminal Sessions

Even if we have no terminal emulator running, several terminal sessions continue to run behind the graphical desktop.

- Access these sessions

  We can access these sessions, called **virtual terminals** or **virtual consoles**, by pressing `Ctrl-Alt-F1` through `Ctrl-Alt-F6` on most Linux distributions.

  When a session is accessed, it presents a login prompt into which we can enter our username and password.

- Switch between these sessions

  To switch from one virtual console to another, press `Alt-F1` through `Alt-F6`.

  On most system we can return to the graphical desktop by pressing `Alt-F7`.
