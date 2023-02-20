# 2. Navigation

## Single File System Tree

- Linux has a single file system tree

  Note that unlike Windows, which has a **separate** file system tree for each storage **device**, Unix-like systems such as Linux always have a **single** file system tree, regardless of how many drives or storage devices are attached to the computer.

- Storage devices are mounted on the tree

  Storage devices are attached (or more correctly, **mounted**) at various points on the tree according to the whims of the system administrator, the person (or people) responsible for the maintenance of the system.

## The Current Working Directory

- `$ pwd`

  To display the current working directory, we use the `pwd` (print working directory) command.

- Home directory

  When we first log in to our system (or start a terminal emulator session) our current working directory is set to our **home directory**.

  Each user account is given its own home directory and it is the only place a regular user is allowed to write files.

## Listing the Contents of a Directory

- `$ ls`

  To list the files and directories in the current working directory, we use the `ls` command.

## Changing the Current Working Directory

- `$ cd pathname`

  To change our working directory we use the `cd` command.

  We can specify pathnames in one of two different ways: as absolute pathnames or as relative pathnames.

- `./` can be omitted

  In almost all cases, we can omit the "./". It is implied.

  Typing `$ cd bin` does the same thing as `$ cd ./bin`.

  In general, if we do not specify a pathname to something, the current working directory will be assumed.

- `cd` shortcuts

  - `$ cd`

    Changes the working directory to your home directory.

  - `$ cd -`

    Changes the working directory to the previous working directory.

  - `$ cd ~user_name`

    Changes the working directory to the home directory of `user_name`.

    For example, `cd ~bob` will change the directory to the home directory of user “bob.”

  - `$ cd -P soft-link`

## Punctuations and Spaces in Filenames

- Limit punctuations in filenames to period, dash, and underscore

  Though Linux supports long filenames that may contain embedded spaces and punctuation characters, limit the punctuation characters in the names of files you create to **period, dash, and underscore**.

- Do not embed spaces in filenames

  Most importantly, **do not embed spaces in filenames**.

  If you want to represent spaces between words in a filename, use underscore characters. You will thank yourself later.
