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

Web browsers: Firefox, Google Chrome, Epiphany, w3m, lynx, and others.
Email clients: Thunderbird, Evolution, Claws Mail, Mutt and mail.
Internet-related tasks: such as Filezilla, XChat, Pidgin, and others.
Office: LibreOffice to create and edit different kinds of documents.
Development applications and tools, including compilers and debuggers.
Sound players: including Amarok, Audacity, and Rhythmbox.
Movie players: including VLC, MPlayer, Xine, and Totem.
Movie editors: including Kino, Cinepaint, Blender among others.
Graphic Tools: GIMP, eog, Inkscape, convert, and Scribus.

## Chapter 7: Command Line Operations

Graphical user interfaces make easy tasks easier, while command line interfaces make difficult tasks possible.

Advantages:

- No GUI overhead is incurred.
- Virtually any and every task can be accomplished while sitting at the command line.
- You can implement scripts for often-used or easy-to-forget tasks and series of procedures.
- You can sign into remote machines anywhere on the Internet.
- You can initiate graphical applications directly from the command line instead of hunting through menus.
- While graphical tools may vary among Linux distributions, the command line interface does not.

```
General usage: command - option - argument
Turn off GUI: `sudo telinit 3`
Turn on GUI: `sudo telinit 5`
Locating application: `which` or `whereis`
Shortcuts for directories: `.` (present directory), `..` (parent directory) and `~` (your home directory)
Absolute paths always start with `/`.
Relative paths never start with `/`.
```

When commands are executed, by default there are three standard file streams open for use:
standard input (standard in or stdin), standard output (standard out or stdout) and standard error (or stderr).
Usually, stdin is your keyboard, and stdout and stderr are printed on your terminal.

Through the command shell, we can redirect the three standard file streams so that we can get input from either a file or another command, instead of from our keyboard, and we can write output and errors to files or use them to provide input for subsequent commands.

If we have a program called do_something that reads from stdin and writes to stdout, we can change its input source by using the less-than sign ( `<` ) followed by the name of the file to be consumed for input data: `do_something < input-file`.
If you want to send the output to a file, use the greater-than sign `>` as in: `do_something 2> error-file`

The UNIX/Linux philosophy is to have many simple and short programs (or commands) cooperate together to produce quite complex results. In order to accomplish this, extensive use of pipes is made. You can pipe the output of one command or program into another as its input.

In order to do this, we use the vertical-bar, `|`, (pipe symbol) between commands as in: `command1 | command2`

`find` is an extremely useful and often-used utility program in the daily life of a Linux system administrator. It recurses down the filesystem tree from any particular directory and locates files that match specified conditions. The default pathname is always the present working directory.

Searching for regular files named gcc: `find /usr -type f -name gcc`
Find and remove all files that end with .swp: `find -name "*.swp" -ok rm {} ’;’`

### Package Management Systems on Linux

The core parts of a Linux distribution and most of its add-on software are installed via the Package Management System. Each package contains the files and other instructions needed to make one software component work well and cooperate with the other components that comprise the entire system. Packages can depend on each other.

There are two broad families of package managers: those based on Debian and those which use RPM as their low-level package manager. The two systems are incompatible, but broadly speaking, provide the same features and satisfy the same needs.

Both package management systems operate on two distinct levels: a low-level tool (such as dpkg or rpm) takes care of the details of unpacking individual packages, running scripts, getting the software installed correctly, while a high-level tool (such as apt-get, yum) works with groups of packages, downloads packages from the vendor, and figures out dependencies.

Most of the time users need to work only with the high-level tool, which will take care of calling the low-level tool as needed. Dependency resolution is a particularly important feature of the high-level tool, as it handles the details of finding and installing each dependency for you.

The Advanced Packaging Tool (apt) is the underlying package management system that manages software on Debian-based systems. While it forms the backend for graphical package managers, such as the Ubuntu Software Center and synaptic, its native user interface is at the command line, with programs that include apt-get and apt-cache.

```
Low Level:
dpkg --list: see all packages
dpkg --list | grep zsh : see zsh package
dpkg --listfiles zsh: see all files of package

High Level:
apt-cache search zsh: show zsh package and its deps
```

## Chapter 8: Finding Linux Documentation

### Use different sources of documentationLinux Documentation Sources

You will need to consult help documentation regularly. Because Linux-based systems draw from a large variety of sources, there are numerous reservoirs of documentation and ways of getting help.

Important Linux documentation sources include:

- The man pages (short for manual pages)
- GNU Info
- The help command and --help option
- Other documentation sources, e.g. Gentoo Handbook or Ubuntu Documentation.

### The man pages

The man pages are the most often-used source of Linux documentation. They provide in-depth documentation about many programs and utilities, as well as other topics. They are present on all Linux distributions and are always at your fingertips.

Typing man with a topic name as an argument retrieves the information stored in the topic's man pages. The man program searches, formats, and displays the information contained in the man page system.

A given topic may have multiple pages associated with it and there is a default order determining which one is displayed when no options or section number is specified. To list all pages on the topic, use `-f`. To list all pages that discuss a specified topic, use the `–k`.

### Access the GNU info System

This is the GNU project's standard documentation format, which it prefers as an alternative to man. The Info System is basically free-form, and supports linked subsections.

Functionally, info resembles man in many ways. However, topics are connected using links (even though its design predates the World Wide Web). Information can be viewed through either a command line interface, a graphical help utility, printed or viewed online.

### Use the help command and --help option

Most commands have an available short description which can be viewed using the --help or the -h option along with the command or application. For example, to learn more about the man command, you can run the following command: `man --help`

The --help option is useful as a quick reference and it displays information faster than the man or info pages.

### Use other documentation sources

In addition to the man pages, the GNU info System, and the help command, there are other sources of Linux documentation, some examples of which include:

Desktop help system: `gnome-help`
Package documentation
Online resources.

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
