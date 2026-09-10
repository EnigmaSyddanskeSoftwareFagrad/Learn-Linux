# *Table of contents*
- [The Linux Filesystem](#the-linux-filesystem)
- [pwd](#pwd)
- [ls](#ls)
- [cd](#cd)
- [cat](#cat)
- [touch](#touch)
- [mkdir](#mkdir)
- [mv](#mv)
- [cp](#cp)
- [rm](#rm)
- [find](#find)
- [sudo](#sudo)
- [chown](#chown)
- [chmod](#chmod)
    * [Permissions](#permissions)
    * [Numeric](#numeric)
    * [Other](#other)
- [man](#man)
- [grep](#grep)
- [less](#less)
- [Pipes](#pipes)
- [Redirection](#redirection)
- [apropos](#apropos)
- [Command Chaining](#command-chaining)
- [Tail and Head](#tail-and-head)

# The Linux Filesystem

Linux has a file structure that will seem familiar and yet unfamiliar if you come from Windows. Files in Linux are structured with the `root` of the filesystem being `/` unlike Windows where you would expect something like `C:\\` as the root. Another difference is the use of `/` (forward slash) on Linux as opposed to `\` (back slash) on Windows.

For you the beginner the folder structure of Linux might seem like complete chaos, but it follows a very sane structure ~~_**for the most part**_~~. 

The most important folders for beginners are `/home` `/bin` `/etc` and `/usr`

* `/home` The home directory is where the home directories for users are stored. *That is to say, any files that are personal to a user are stored within a folder that commonly bears the name of the user.

* `/bin` The bin directory where program binaries are stored. If you don't know what a binary is, then there is no reason to worry, you only have to think of them as programs. The bin directory among other locations is included in the path environment variable. This means that any programs which can be found on the path can be run without pointing to them explicitly. An example could be ```/bin/cat```, which would be how we would have to call ```cat``` if we did not have /bin in the path variable, but with it, in place, we can simply call `cat`, as is, to execute the program.

* `/etc` The etc directory is where configuration files are stored. These configuration files impact the whole system and as such ones specific to a user are stored within that user's home directory. When working with setup and services you are likely to run into the etc folder and the configs within.

* `/usr` Finally among the folders you are likely to encounter first is the usr directory. This directory is where user utilities and programs are installed. If you were to develop a program and wanted to make it available to all users, this is where you would put it. Within the directory, you will also find a bin folder for storing the user program binaries the same way as with the /bin folder.

---
## pwd
The first step of your Linux command line journey is to know where you are. For this, we have the command ```pwd``` which stands for _**p**rint **w**orking **d**irectory_. This command will as it says tell you where in the directory structure you are. Using the command requires nothing but entering it and hitting enter.
```bash
pwd
```

## ls
The next step after finding out where you are would be to have a look around. To see what is in a folder the command to use would be ```ls``` which is short for _list_ as it lists the contents of a directory. 

`ls` is used in different ways. You can use it without specifying a directory which will yield the contents of the current directory. You can also specify a directory for which it should display its contents.
```bash
ls
```

```bash
ls ./first-folder/inner-folder
```

We also have options that we can add to the command.  A very common combination of options is `-l -a` or just `-la`.  This combination of options will show all the files in a list format that also shows other information about the files such as owners, size, permissions and more.

Showing files is more of a thing as some files and folders get hidden in the normal ls if they begin with a `.`

```bash
ls -la ./first-folder
```

## cd

Knowing where we can go is great for our next step into the file-system. To navigate the file-system we have the command ```cd``` which is short for _**C**hange **D**irectory_. Using ```cd``` we can change where we are in the file-system.

To use the `cd` command we specify where we want to go.
```bash
cd first-folder
```

```bash
cd /home/enigma/first-folder
```

## cat
Now that we know how to traverse the file-system, we can start interacting with the files. 
One of the first things we might want could be to see the contents of a file. 
To do this we can use the ```cat``` command. ```cat``` is short for _concatenate_.

To use `cat` we specify the file that we want the contents of.
```bash
cat /home/enigma/first-folder/important-document.txt
```

## touch

With the ability to navigate and explore files we need the ability to create them as well. To create a file we have the touch command. This command will create an empty file where you have specified.

To create a file using touch we specify the file that we want to create where we want to create it.

Assuming that the file important-document.txt does not exist within the folder first-document, we can create it with the following command.
```bash
touch 
```

## mkdir
We now have to knowledge to create file, so now we will explorer the creation of folders. To create a folder we use the command `mkdir` which is short form for _Make Directory_. 

## mv
With both files and folder creation within our grasp, moving them around and renaming them becomes our next priority. To move files around we use the ```mv``` command which is short for _Move_.

To use the move command to move a file we first specify the file that we want to move, and then we specify where we want to move it. 
```bash
mv /home/enigma/first-folder/important-document.txt /home/enigma/second-folder
```

If we want to rename a file we do it much the same way. The difference however lies in how we specify where the file goes. When specifying where the file goes we also specify the new filename.
```bash
mv /home/enigma/first-folder/important-document.txt /home/enigma/first-folder/important-document-new-name.txt
```

## cp
While moving is nice and all, we might want to have copies as well. To copy something we use the ```cp``` command, which is short for _Copy_. The copy command works much the same as the move command in that it allows you to both copy a file or directory to another directory but also specify a new name for the file or directory that you are copying.

Copy without changing the name:

```bash
cp /home/enigma/first-folder/important-document.txt /home/enigma/second-folder
```

Copy with a new name:

```bash
cp /home/enigma/first-folder/important-document.txt /home/enigma/first-folder/important-document-new-name.txt
```

When copying a folder, only the folder itself will be copied, the contents will not be copied. To also copy the contents we need to specify an option on the copy command. The option in question is the recursive option or `-r`.

To use this option in the command, we simply add it as the first thing after the command.
```bash
cp -r /home/enigma/first-folder /home/enigma/third-folder
```

## rm
Now that we have strewn the filesystem with all of our new files and folder we need a way to delete them. To delete files and folders we have the `rm` command which is short for _Remove_. 

To remove a file we simply specify which file we would like to remove.
```bash
rm /home/enigma/first-folder/important-document.txt
```

Deleting folders, however, requires the use of the recursive option. 
This is the case for any folder no matter if it contains files or not.
```bash
rm -r /home/enigma/first-folder
```

## find

Having control of files and their contents is good and all, but your average filesystem is extremely expansive. As such looking through every folder one at a time for the file you need can be very time-consuming and difficult. To solve this problem we have the program `find`. It will look through every folder that you have access to in search of the file you are looking for.

To use the find command we first specify where to search. i.e. if you want to look everywhere we specify the root /. We can also specify multiple locations by separating them with a space. The second thing we specify is the name of the file that we are looking for. To specify this we add '-name' and then the name of the file that you are looking for encased in quotes.

_Search for a file from root up called important-document.txt_
```bash
find / -name 'important-document.txt'
```

To get a faster and more interactive file finder, we recommend using `fzf` which is a fuzzy finder for files. 

## sudo

When working within Linux, you are likely to encounter many things that you do not have the correct level of access to. Many things require you to have access to the root user. This, however, would require everyone with admin rights to know a common password for the root account.

This is far from convinient and makes it harder to manage access. To fix this the ```sudo``` program comes into play. _sudo_ stands for _**S**uper **U**ser **DO**_. By prepending `sudo` to the front of your commands, they will be run as the root user instead of yourself. This is useful for things like installing programs or changing system configurations that are owned by the root user.
A caveat on using sudo is that you need to be registered in the sudo group to be able to run commands using sudo.

## chown

Now that we have covered the most important things for a beginner, we can continue our journey into the more complex parts of Linux.
As we have discussed in the earlier exercises, ownership is a thing. This counts for both files as well as directories.

To change the ownership of a file you will often need to use sudo as the instances where you need to change ownership usually coincide with you not having the ownership. Files and directories in Linux have two types of ownership. There is the user that owns the file, but there is also a group that is associated with the file.

To change the ownership of a file using sudo, you can use this command.
```bash
sudo chown enigma:enigma-users /home/enigma/first-folder/important-document.txt
```

This command starts with the `sudo` command to run the `chown` command with administrator rights, then comes the `chown` command itself. The first thing specified in the `chown` command is the new owners specified as `user:group` where the username and the group name are separated using a single colon. Any further arguments added at the end of the command specify files that should receive the new ownership information. These files are separated with spaces.

## chmod
While knowing about ownership is good, there is more to accessing files than just that. Files and folders have something called modes. Modes describe whether the owner, the group or others can read, write or execute a file. The Mode is assigned individually for the owner, the group and others.

When using the command `ls -la` we are presented with results that also show the modes for the files and folders present. This is an example of the output.
```bash
total 120
drwxr-xr-x  3 enigma enigma  4096 Sep  6 20:27 .
drwxr-xr-x  4 root   root    4096 Sep  6 20:14 ..
-rw-------  1 enigma enigma   213 Sep  6 20:20 .bash_history
-rw-r--r--  1 enigma enigma   220 Apr 18 20:19 .bash_logout
-rw-r--r--  1 enigma enigma  3526 Apr 18 20:19 .bashrc
-rw-r--r--  1 enigma enigma    89 Sep  6 20:25 hello_world.cpp
-rwxr-xr-x  1 enigma enigma 16544 Sep  6 20:26 hello_world_program
drwxr-xr-x 12 enigma enigma  4096 Sep  6 20:20 .oh-my-zsh
-rw-r--r--  1 enigma enigma   807 Apr 18 20:19 .profile
-rw-r--r--  1 enigma enigma 50765 Sep  6 20:22 .zcompdump-testmachine.5.8
-rw-r--r--  1 enigma enigma  3858 Sep  6 20:21 .zshrc
-rw-r--r--  1 enigma enigma    29 Sep  6 20:19 .zshrc.pre-oh-my-zsh
```

On the left, we see a bunch of letters and dashes. The left-most letter is `d` if the item is a directory or a `-` if it is a file. The next three letters describe the Modes for the user, followed by three for groups mode, and three for the mode for others.

The letters have the following meanings:
* `r` - This means `read` and if specified gives read permissions. Read permission means being able to see the contents of a folder, or being able to read the contents of a file.
* `w` - This means `write` and if specified permits changing the contents of a file or adding files to a directory.
* `x` - This means `execute` and specifies that a file can be run as code or that a directory can be traversed. 

These file permissions can also be described with a single number for the user, the group and others. An example could be `754` where `7` is the permissions for the user, `5` for the group and `4` for others.

The modes each have a numerical value, that is summed up to give the mode.

| Combination        | Symbol | Octal Sum calculation | Description              |
| :----------------- | :----: | :-------------------- | :----------------------- |
| **Full Access**    | `rwx`  | 4 + 2 + 1 = **7**     | Read, Write, and Execute |
| **Read & Write**   | `rw-`  | 4 + 2 + 0 = **6**     | Read and Write only      |
| **Read & Execute** | `r-x`  | 4 + 0 + 1 = **5**     | Read and Execute only    |
| **Read Only**      | `r--`  | 4 + 0 + 0 = **4**     | Read access only         |
| **Write Only**     | `-w-`  | 0 + 2 + 0 = **2**     | Write access only        |
| **Execute Only**   | `--x`  | 0 + 0 + 1 = **1**     | Execute access only      |
| **No Access**      | `---`  | 0 + 0 + 0 = **0**     | Nothing allowed          |

These are binary flags.
If you want to give a file read and write, you activate the read and write bit resulting in 0b110 or 6.

### Permissions
When assigning permissions there are two ways of doing it. You can assign the permissions by specifying the three-digit value for the permissions. The other way is to use a more complicated syntax that let you change different parts separately. The program that is used to assign permissions is called `chmod` which is a contraction of _change mode_

### Numeric
When assigning the numeric way we use the following command:
```bash
chmod 754 /home/enigma/first-folder/important-document.txt
```

The command starts by specifying the permissions we want to set, followed by a list of files and or folders that we want to set the permissions for. It is also possible to specify that the changes should be made recursively if done on a folder. 

This is done with the option `-R` placed just after the command itself
```bash
chmod -R 754 /home/enigma/first-folder
```

### Other
The other way involves firstly specifying who you want to change permissions for. This is done with four different letter. `u` for user, `g` for group, `o` for other, and `a` for all. You can also omit to specify the first letter, which will be the same as using `a`. The second thing we specify is how we want to change the permissions. We can add with `+`, subtract with `-` or set to exactly with `=`. The third thing specified are the permissions that we are setting.

This will add the permissions x and r to the users mode without affecting the other modes
```bash
chmod u+xr ./important-document.txt
```

This will remove the execute permission from the group and others without affecting the users modes
```bash
chmod go-x ./important-document.txt
```

This will set the groups mode to exactly `rx` without affecting the modes of the user and other
```bash
chmod g=rx
```

## man
After seeing the complexities of many of the previous commands, you are probably wondering how you are going to remember how everything works. For that, we have the `man` command which is short for _manual_. It is very simple to use the `man` command. We simply prepend man to any command that we wish to have the manual for and voila a manual will be presented.

Navigate the manual we use the arrow keys, and to quit the manual we hit `q`

An example could be:
```bash
man chmod
```

Or
```bash
man man
```

## grep

`Grep` is another awesome tool. It will allow us to search the contents of a file.
```bash
grep "secret phrase" ./important-file.txt
```

## less

Less is also one of the many great tools available, and you have in fact already met this tool. When we invoke `man` it, in turn, invokes `less` to show us the contents of the manual in a navigable way.

When less is invoked it takes the contents of the file and brings it into a view that is navigable with the arrow keys instead of just dumping it into the terminal like `cat` does.
To invoke less we give less the file we want to see as argument.
```bash
less ./important-file.txt
```

## Pipes
One of the main tenets of Linux is to make every program a filter. This means that programs should be able to use take the input of other programs and send their results on afterwards to the next program. To achieve this we have standard out and standard in. These are something called a pipe, and can be thought of like a queue.

Standard in is a pipe that represents input, and standard out represents output. When a program outputs non error output, it is most often done using standard out. Likewise many programs like `less` can take standard in as well. To pipe between programs like this, we join them with the pipe symbol `|`. An example could be if ls had a very long output that was hard to see in the terminal. 

We would then be able to pipe the results into less to be able to explore them like this.
```bash
ls -la | less
```

This way the output of ls is given to less as if it was a file and less is able to display it.
Most other programs work in the same way and can, as such, be chained.

## Redirection
It is also possible to redirect the output to a file. If we redirect the output using `>` we can write the output to said file. Using `>` will create the file if it does not already exist and will override an existing file. If we want to append the output to the file instead, we use `>>`.

```bash
ls -A1 > files_here.txt
```

## apropos
Now that you have seen an extreme amount of commands, you might think: "how am I supposed to know which command to use." Fret not. We have the `apropos` command. It will search the man pages for what you want to know. 

As an example, if you wanted to know something about PDF, you would type the following:
```bash
apropos pdf
```

It will then return the titles for all the man pages that reference PDF. You can then go through the pages one by one to see if the specific thing does what you want.

## Command Chaining
Some commands take a while to run, as such you might want to have something run after the first command is done. To do this we have the semicolon. 

It can be put at the end of a command and allow you to chain another command right after.
```bash
touch testfile; chmod 600 ./testfile; echo "Secrets" > testfile
```

This way we can create a file, change the permissions for the file, and then add some text to it without having to way for each command to finish.

We might however limit the commands to only run if the previous command succeeded. To do this we combine the command with `&&` instead of `;`. This way the second command won't be run unless the first one succeeded. Similarly, we might want to run something only if the previous command failed, and for that, we have `||`

## Tail and Head
Finally for this lesson we have the utilities `head` and `tail`, which, much like cat, returns the contents of a file. However, they only return a certain number of lines from either the beginning or end of the file.

```bash
head files_here.txt -n 1
```

Here we use the option -n to specify how many lines we want (in this case 1).
Tail works the exact same way, it will just return the last line instead.

```bash
tail files_here.txt -n 1
```
