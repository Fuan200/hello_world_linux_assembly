# Hello World with Assembly on Linux

This is a simple example of how to make a Hello World in assembly on using Linux as the OS.

## OS

Linux

## Programming Language

Assembly

### Architecture

x86_64 or x86 : intel or amd

## Prerequisites

* A distribution of Linux x86_64
* nasm (netwide assembler: it is an assembler for x86 and x86-64 architectures, used to write assembly language code):
  * Debian:
    ```
    sudo apt install nasm
    ```
  * Alpine:
    ```
    sudo apk add nasm
    ```
  * Fedora:
    ```
    sudo dnf install nasm
    ```
  * Arch:
    ```
    sudo pacman -S nasm
    ```

* ld (command in linux is a link editor, ld [ options ] inputfile outputfile. It combines object and archive files to create an executable)

## Getting Started

1. Clone the repository:

``` shell
git clone git@github.com:Fuan200/hello_world_linux_assembly.git
```

2. Move to directory

``` shell
cd hello_world_linux_assembly
```

3. Execute

``` shell
nasm -f elf64 -o hello_world.o hello_world.asm

ld -o hello_world hello_world.o

./hello_world
```

### Run a file with a single command

To execute the assembly code with a single command, we will create a bash command for this purpose.

The code for the script(sh):

``` bash
#!/bin/bash

if [ "$#" -ne 1 ]; then
    echo "Usage: make_assemble <file.asm>"
    exit 1
fi

filename=$(basename -- "$1")
filename="${filename%.*}"

nasm -f elf64 -o "$filename.o" "$1"

ld -o "$filename" "$filename.o"

./"$filename"
```

First check if the number of arguments passed to the script is not equal to 1, because the script need 1 argument, show how usage and end the script is not equal to 1.

`filename=$(basename -- "$1")`: This line uses the basename command to extract the filename from the path provided as the first argument ($1). It removes any directory components from the path and stores just the filename in the filename variable.

`filename="${filename%.*}"`: This line uses parameter expansion to remove the extension from the filename stored in the filename variable. ${filename%.*} removes the shortest match of .* (i.e., the extension) from the end of the string in filename. The result is the filename without the extension.

And later make the executable file.

#### Command Activation

1. Change the permissions of the script `make_assemble.sh`

``` shell
chmod +x make_assemble.sh
```

2. Move the script to path `usr/local/bin`:

``` bash
sudo mv make_assemble.sh /usr/local/bin/make_assemble
```

3. Open a new terminal:

``` bash
make_assemble hello_world.asm
```

4. Output:

```
Hello World!!!
```

## Author

:blue_heart: **Juan Antonio Díaz Fernández** - [Fuan200](https://github.com/Fuan200)