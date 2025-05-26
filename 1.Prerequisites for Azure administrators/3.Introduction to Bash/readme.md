# Introduction to Bash

> Bash is the standard shell scripting language for Linux. Let's learn the basics of Bash, starting with the syntax and commonly used commands, like ls and cat.

## What is Bash?

1. Bash is a vital tool for managing Linux machines. The name is short for "Bourne Again Shell."
2. A shell is a program that commands the operating system to perform actions. You can enter commands in a console on your computer and run the commands directly, or you can use scripts to run batches of commands. Shells like PowerShell and Bash give system administrators the power and precision they need for fine-tuned control of the computers they're responsible for.

## Bash fundamentals

The full syntax for a Bash command is:

```bash
command [options] [arguments]
```

---

Example bash commands:

```bash
ls
ls /etc
ls -a /etc
ls -al /etc
man mkdir
ls *.png
ls *.jpg *.jpeg
ls *.jp*g
ls 000?.jpg
ls *.[jp]*
ls *.[jpJP]*
ls [a-z]*
ls [A-Z]*
ls [a-zA-Z]*
ls [0-9]*
ls *[0-9]*
ls *[0-9]
$ ls *\**
```

## Bash commands and operators

### Bash commands

#### ls command

- ls lists the contents of your current directory or the directory specified in an argument to the command. By itself, it lists the files and directories in the current directory.

#### cat command

- Suppose you want to see what's inside a file. You can use the cat command for that. The output won't make much sense unless the file is a text file.

```bash
cat /etc/os-release
```

#### sudo command

- Some Bash commands can only be run by the root user; a system administrator or superuser. If you try one of these commands without sufficient privileges, it fails.

#### cd, mkdir, and rmdir commands

- cd stands for "change directory," and it does exactly what the name suggests: it changes the current directory to another directory. It enables you to move from one directory to another just like its counterpart in Windows.

```bash
cd orders
cd ..
cd ~
mkdir orders
mkdir --parents orders/2019
rm 0001.jpg
rm *
rm -i *
rm -r orders
```

#### cp command

- The cp command copies not just files, but entire directories (and subdirectories) if you want. To make a copy of 0001.jpg named 0002.jpg

```bash
cp 0001.jpg 0002.jpg
cp -i 0001.jpg 0002.jpg
cp * photos
cp photos/* images
cp -r photos images
```

#### ps command

- The ps command gives you a snapshot of all the currently running processes. By itself, with no arguments, it shows all your shell processes

```bash
ps -e
ps -ef
ps aux
```

#### w command

- To find out who's on your servers, Linux provides the w (for "who") command. It displays information about the users currently on the computer system and those users' activities. w shows user names, their IP addresses, when they logged in, what processes they're currently running, and how much time those processes are consuming. It's a valuable tool for sysadmins.

#### Bash I/O operators

- You can do a lot in Linux just by exercising Bash commands and their many options. But you can really get work done when you combine commands by using I/O operators:

  - < for redirecting input to a source other than the keyboard
  - \> for redirecting output to destination other than the screen
  - \>> for doing the same, but appending rather than overwriting
  - | for piping output from one command to the input of another

```bash
ls > listing.txt
ls >> listing.txt
ps -ef | more
ps -ef | head
ps -ef | grep daemon
sort < file.txt
sort < file.txt > sorted_file.txt
cat file.txt | fmt | pr | lpr
```
