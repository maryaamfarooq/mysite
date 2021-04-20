---
title: "Explanation"
date: 2021-04-20T00:25:43+05:00
draft: true
feature_image: "/dir/blue2.jpg"
summary: "Making a 64-bit OS"
---
#### Building 64-bit Operating System from scratch.

--------------------------------------------------------

The 64-bit x86 operating system kernel is multiboot2-compliant.

It includes boot code and a multiboot2 header so that it can be understood by bootloaders.

This operating system has been primarily written in C, but also includes assembly for the hardware-specific code.

__Tools used__

- A text editor such as _Visual Studio Code_

- _Docker_ for creating the build environment

- _Qemu_ for emulating the OS

__Essential Files__

1. Dockerfile

This file contains:
  - all the steps needed to create our build environment image. The image is based on a pre-made image which contains all the gcc compilation tools that are needed.
  - a command to install nasm which is used to compile the assembly code.
  - the grub package for building the final iso file

Once the image has been made, an instance of it is spinned up which is known as a container.

2. header.asm

This assembly file contains data which is to be included in the operating system binary. This magic data is necessary so that bootloaders can understand that we have an operating system here that can be run on your computer.
It specifies some information about the OS, i.e., protected mode.

3. main.asm

This is the entry point to our operating system. 

It also contains the code to convert the 32-bit operating system to 64-bit for task 2.

4. linker.ld

The files desrcibes how to link the operating system together and sets the current address to 1MB for the kernels to be loaded by the bootloader. It also includes the mulit-boot header.

5. grub.cfg

This creates an iso file out of our operating system kernel binary. It also defines the name of the operating system.

6. Makefile

It ensures that only files that have been modified get rebuilt. It also includes variables to hold all the assembly source files and assembly object files and contains the commands to build the object files from the corresponding source file when it is modified. The assembly source files are compiled by nasm.

7. kernel.iso

This is final iso file created by running the _make build-x86_64_ command.

8. main.c

A function names _kernel_main_ is created which is then called in the assembly code. It also contains function like _clr()_ (to clear the screen), _set_color_ (to change background and foreground colors), and a function to print text and display it on the screen, etc.

9. print.h

This is the header file that is inlcuded in the other _.c_ files.

10. print.c

This is the implemenation file that contains the definition for all the functions mentioned above.
