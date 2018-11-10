# LinuxFoundationX: LFS101x Introduction to Linux

Source: https://courses.edx.org/courses/course-v1:LinuxFoundationX+LFS101x+3T2018/course/

## Chapter 1: The Linux Foundation

### Discuss the role of The Linux Foundation

The Linux Foundation is the umbrella organization for many critical open source projects that power corporations, spanning all industry sectors. Its work today extends far beyond Linux, fostering innovation at every layer of the software stack.

### Describe the three major Linux distribution families

Red Hat Family Systems (including CentOS and Fedora)
SUSE Family Systems (including openSUSE)
Debian Family Systems (including Ubuntu and Linux Mint).

## Chapter 2: Linux Philosophy and Concepts

Linux borrows heavily from the UNIX operating system, with which its creators were well-versed.
Linux accesses many features and services through files and file-like objects.
Linux is a fully multi-tasking, multi-user operating system, with built-in networking and service processes known as daemons.
Linux is developed by a loose confederation of developers from all over the world, collaborating over the Internet, with Linus Torvalds at the head. Technical skill and a desire to contribute are the only qualifications for participating.
The Linux community is a far reaching ecosystem of developers, vendors, and users that supports and advances the Linux operating system.

### Define the common terms associated with Linux

Kernel: glue between hardware and applications
Distribution: collection of software, combined with the Linux Kernel, making up a Linux-based Operating System
Bootloader: program that boots the Operating System
Service: program that runs as a background process
Filesystem: method for storing and organizing files
X Window System: graphical subsystem on nearly all Linux systems
Desktop Environment: graphical user interface on top of the OS
Command Line: interface for typing commands on top of the OS
Shell: Command Line Interpreter that interprets the Command Line input and instructs the OS to perform any tasks and command

## Chapter 3: Linux Basics and System Startup

### Identify the differences between partitions and filesystems

A partition is a physically contiguous section of a disk, or what appears to be so.
A filesystem is a method of storing/finding files on a hard disk (usually in a partition).
One can think of a partition as a container in which a filesystem resides, although in some circumstances, a filesystem can span more than one partition if one uses symbolic links, which we will discuss much later.

### Describe the boot process

Power On
BIOS: Initialize hardware, test memory
MBR: boot loader is stored in boot sector or efi partition
Boot Loader: load kernel image and initial Ram Disk
Kernel: initialize and configure memory and all hardware
Initial Ram Disk: load filesystem, drivers
sbin/init (systemd now): init program of root filesystem
Command Shell using getty: User Login
X Windows System

## Chapter 4: Graphical Interface

You can use either a Command Line Interface (CLI) or a Graphical User Interface (GUI) when using Linux.

To work at the CLI, you have to remember which programs and commands are used to perform tasks, and how to quickly and accurately obtain more information about their use and options. For repetitive tasks, the CLI is often more efficient.

Using the GUI is often quick and easy. It allows you to interact with your system through graphical icons and screens. The GUI is easier to navigate if you do not remember all the details or do something only rarely.

X Window System: Display Manager: A service called the display manager keeps track of the displays being provided and loads the X server (it provides graphical services to applications). The display manager also handles graphical logins and starts the appropriate desktop environment after a user logs in.

If the display manager is not started by default in the default runlevel, you can start X a different way, after logging on to a text-mode console, by running startx from the command line. Or, you can start the display manager (gdm, lightdm, kdm, xdm, etc.) manually from the command line.

A desktop environment consists of a session manager, which starts and maintains the components of the graphical session, and the window manager, which controls the placement and movement of windows, window title-bars, and controls.

GNOME is a popular desktop environment with an easy-to-use graphical user interface. It is bundled as the default desktop environment for most Linux distributions. Another common desktop environment very important in the history of Linux and also widely used is KDE, which has often been used in conjunction with SUSE and openSUSE.

## Chapter 5: System Configuration from the Graphical Interface

### Install and update software in Linux from a graphical interface

Each package in a Linux distribution provides one piece of the system, such as the Linux kernel, or the Firefox web browser.

Packages often depend on each other. For example, because Firefox can communicate using SSL/TLS, it will depend on a package which provides the ability to encrypt and decrypt SSL and TLS communication, and will not install unless that package is also installed at the same time.

One utility handles the low-level details of unpacking a package and putting the pieces in the right places. Most of the time, you will be working with a higher-level utility which knows how to download packages from the Internet and can manage dependencies and groups for you.

Debian: dpkg is the underlying package manager for these systems. It can install, remove, and build packages. Unlike higher-level package management systems, it does not automatically download and install packages and satisfy their dependencies. For Debian-based systems, the higher-level package management system is the apt (Advanced Package Tool) system of utilities. While each distribution within the Debian family uses apt, it creates its own user interface on top of it (e.g. apt-get, aptitude, Ubuntu Software Center, etc). Although apt repositories are generally compatible with each other, the software they contain generally is not. Therefore, most apt repositories target a particular distribution (like Ubuntu), and often software distributors ship with multiple repositories to support multiple distributions.

Red Hat Package Manager (RPM): The high-level package manager differs between distributions: Red Hat family distributions have historically used the repository format used by yum (Yellowdog Updater, Modified), although recent Fedora uses a replacement, dnf, still using the same format. SUSE family distributions also use RPM, but use the zypper interface.

## Chapter 6: Common Applications

## Chapter 7: Command Line Operations

## Chapter 8: Finding Linux Documentation

## Chapter 9: Processes

## Chapter 10: File Operations

## Chapter 11: Text Editors

## Chapter 12: User Environment

## Chapter 13 : Manipulating Text

## Chapter 14: Network Operations

## Chapter 15 : The Bash Shell and Basic Scripting

## Chapter 16: More on Bash Shell Scripting

## Chapter 17: Printing

## Chapter 18: Local Security Principles
