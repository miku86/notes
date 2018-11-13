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

### Describe what a process is and distinguish between types of processes

Processes are used to perform various tasks on the system.
Processes can be single-threaded or multi-threaded.
Processes can be of different types, such as interactive and non-interactive.
Every process has a unique identifier (PID) to enable the operating system to keep track of it.
The nice value, or niceness, can be used to set priority.
ps provides information about the currently running processes.
You can use top to get constant real-time updates about overall system performance, as well as information about the processes running on the system.
Load average indicates the amount of utilization the system is under at particular times.
Linux supports background and foreground processing for a job.
at executes any non-interactive command at a specified time.
cron is used to schedule tasks that need to be performed at regular intervals.

A process is simply an instance of one or more related tasks (threads) executing on your computer. It is not the same as a program or a command. A single command may actually start several processes simultaneously. Some processes are independent of each other and others are related. A failure of one process may or may not affect the others running on the system.

Processes use many system resources, such as memory, CPU cycles, and peripheral devices. The operating system (especially the kernel) is responsible for allocating a proper share of these resources to each process and ensuring overall optimized system utilization.

### Types of Processes

Interactive Processes: Need to be started by a user, either at a command line or through a graphical interface such as an icon or a menu selection. bash, firefox.

Batch Processes: Automatic processes which are scheduled from and then disconnected from the terminal. These tasks are queued and work on a FIFO basis. updatedb.

Daemons: Server processes that run continuously. Many are launched during system startup and then wait for a user or system request indicating that their service is required. httpd, xinetd, sshd.

Threads: These are tasks that run under the umbrella of a main process, sharing memory and other resources, but are scheduled and run by the system on an individual basis. An individual thread can end without terminating the whole process and a process can create new threads at any time. Many non-trivial programs are multi-threaded. firefox, gnome-terminal-server.

Kernel Threads: Kernel tasks that users neither start nor terminate and have little control over. These may perform actions like moving a thread from one CPU to another, or making sure input/output operations to disk are completed. kthreadd, migration, ksoftirqd

#### Process Scheduling and States

A critical kernel function called the scheduler constantly shifts processes on and off the CPU, sharing time according to relative priority, how much time is needed and how much has already been granted to a task.

When a process is in a so-called running state, it means it is either currently executing instructions on a CPU, or is waiting to be granted a share of time (a time slice) so it can execute. All processes in this state reside on what is called a run queue and on a computer with multiple CPUs, or cores, there is a run queue on each.

However, sometimes processes go into what is called a sleep state, generally when they are waiting for something to happen before they can resume, perhaps for the user to type something. In this condition, a process is sitting on a wait queue.

There are some other less frequent process states, especially when a process is terminating. Sometimes, a child process completes, but its parent process has not asked about its state. Amusingly, such a process is said to be in a zombie state; it is not really alive, but still shows up in the system's list of processes.

To terminate a process, you can type `kill -9 <pid>`.
Put process in background: `<process> &`
See all processes: `ps -u`
Taskmanager: `top`

### Use at, cron, and sleep to schedule processes in the future or pause them

cron is a time-based scheduling utility program. It can launch routine background jobs at specific times and days on an on-going basis. cron is driven by a configuration file called /etc/crontab (cron table), which contains the various shell commands that need to be run at the properly scheduled times. There are both system-wide crontab files and individual user-based ones. Each line of a crontab file represents a job, and is composed of a so-called CRON expression, followed by a shell command to execute.

The crontab -e command will open the crontab editor to edit existing jobs or to create new jobs.

sleep and at are quite different; sleep delays execution for a specific period, while at starts execution at a later time.

```
Example:

Set up a cron job to do some simple task every day at 10 AM.

Create a file named mycrontab with the following content: 0 10 * * * /tmp/myjob.sh

Create /tmp/myjob.sh containing:
#!/bin/bash
echo Hello I am running $0 at $(date)

Make it executable: chmod +x /tmp/myjob.sh

Put it in the crontab system with: crontab mycrontab

Verify it was loaded with: crontab -l

You can remove it with: crontab -r
```

## Chapter 10: File Operations

### Explore the filesystem and its hierarchy

In Linux it is often said “Everything is a file”, or at least it is treated as such. This means whether you are dealing with normal data files and documents, or with devices such as sound cards and printers, you interact with them through the same kind of Input/Output (I/O) operations. This simplifies things: you open a “file” and perform normal operations like reading the file and writing on it.

On many systems, the filesystem is structured like a tree. The tree is usually portrayed as inverted, and starts at what is most often called the root directory, which marks the beginning of the hierarchical filesystem and is simply denoted by /. The root directory is not the same as the root user. The hierarchical filesystem also contains other elements in the path (directory names), which are separated by forward slashes (/), as in /usr/bin/emacs, where the last element is the actual file name.

Linux supports a number of native filesystem types, expressly created by Linux developers, such as: ext3, ext4, squashfs, btrfs.

It also offers implementations of filesystems used on other alien operating systems, such as those from: Windows (ntfs, vfat), SGI (xfs), IBM (jfs), MacOS (hfs, hfs+).

It is often the case that more than one filesystem type is used on a machine, based on considerations such as the size of files, how often they are modified, what kind of hardware they sit on and what kind of access speed is needed, etc. The most advanced filesystem types in common use are the journaling varieties: ext4, xfs, btrfs, and jfs. These have many state-of-the-art features and high performance, and are very hard to corrupt accidentally.

Each filesystem on a Linux system occupies a hard disk partition. Partitions help to organize the contents of disks according to the kind and use of the data contained. For example, important programs required to run the system are often kept on a separate partition (known as root or /) than the one that contains files owned by regular users of that system (/home). In addition, temporary files created and destroyed during the normal operation of Linux may be located on dedicated partitions. One advantage of this kind of isolation by type and variability is that when all available space on a particular partition is exhausted, the system may still operate normally.

Before you can start using a filesystem, you need to mount it to the filesystem tree at a mount point. This is simply a directory (which may or may not be empty) where the filesystem is to be attached (mounted). Sometimes, you may need to create the directory if it does not already exist.

The mount command is used to attach a filesystem somewhere within the filesystem tree. The basic arguments are the device node and mount point.

`sudo mount /dev/sda5 /home` will attach the filesystem contained in the disk partition associated with the /dev/sda5 device node, into the filesystem tree at the /home mount point. There are other ways to specify the partition other than the device node, such as using the disk label or UUID.

To unmount the partition, the command would be: `sudo umount /home`

If you want it to be automatically available every time the system starts up, you need to edit /etc/fstab accordingly. Looking at this file will show you the configuration of all pre-configured filesystems. man fstab will display how this file is used and how to configure it.

Typing `mount` without any arguments will show all presently mounted filesystems.

The command `df -Th` will display information about mounted filesystems, including the filesystem type, and usage statistics about currently used and available space.

### Explain the filesystem architecture

Each user has a home directory, usually placed under /home. The /root ("slash-root") directory on modern Linux systems is no more than the home directory of the root user.

On multi-user systems, the /home directory infrastructure is often mounted as a separate filesystem on its own partition, or even exported (shared) remotely on a network.

Sometimes, you may group users based on their department or function. You can then create subdirectories under the /home directory for each of these groups.

The /bin directory contains executable binaries, essential commands used to boot the system or in single-user mode, and essential commands required by all system users, such as cat, cp, ls, mv, ps, and rm. Likewise, the /sbin directory is intended for essential binaries related to system administration, such as fsck and shutdown.

Commands that are not essential (theoretically) for the system to boot or operate in single-user mode are placed in the /usr/bin and /usr/sbin directories. Historically, this was done so /usr could be mounted as a separate filesystem that could be mounted at a later stage of system startup or even over a network. However, nowadays most find this distinction is obsolete. In fact, many distributions have been discovered to be unable to boot with this separation, as this modality had not been used or tested for a long time. Thus, on some of the newest Linux distributions /usr/bin and /bin are actually just symbolically linked together, as are /usr/sbin and /sbin.

Certain filesystems, like the one mounted at /proc, are called pseudo-filesystems because they have no permanent presence anywhere on the disk. The /proc filesystem contains virtual files (files that exist only in memory) that permit viewing constantly changing kernel data. This filesystem contains files and directories that mimic kernel structures and configuration information. It does not contain real files, but runtime system information, e.g. system memory, devices mounted, hardware configuration, etc.

The /dev directory contains device nodes, a type of pseudo-file used by most hardware and software devices, except for network devices. This directory is empty on the disk partition when it is not mounted and contains entries which are created by the udev system, which creates and manages device nodes on Linux, creating them dynamically when devices are found.

The /var directory contains files that are expected to change in size and content as the system is running, such as System log files: /var/log, Packages and database files: /var/lib, Print queues: /var/spool, Temporary files: /var/tmp.

The /etc directory is the home for system configuration files. It contains no binary programs, although there are some executable scripts. For example, /etc/resolv.conf tells the system where to go on the network to obtain host name to IP address mappings (DNS). Files like passwd, shadow and group for managing user accounts are found in the /etc directory. While some distributions have historically had their own extensive infrastructure under /etc, with the advent of systemd there is much more uniformity among distributions today.

The /boot directory contains the few essential files needed to boot the system. For every alternative kernel installed on the system there are four files: vmlinuz (the compressed Linux kernel, required for booting), initramfs (the initial ram filesystem, required for booting, sometimes called initrd), config (the kernel configuration file, only used for debugging and bookkeeping), System.map (Kernel symbol table, only used for debugging). The GRUB files such as /boot/grub/grub.conf or /boot/grub2/grub2.cfg are also found under the /boot directory.

/lib contains libraries for the essential programs in /bin and /sbin. These library filenames either start with ld or lib. For example, /lib/libncurses.so.5.9. Most of these are what is known as dynamically loaded libraries (also known as shared libraries or Shared Objects (SO)).

Most Linux systems are configured so any removable media are automatically mounted when the system notices something has been plugged in. While historically this was done under the /media directory, modern Linux distributions place these mount points under the /run directory. For example, a USB pen drive with a label "myusbdrive" for a user name "student" would be mounted at /run/media/student/myusbdrive. The /mnt directory has been used since the early days of UNIX for temporarily mounting filesystems. These can be those on removable media, but more often might be network filesystems with NFS, which are not normally mounted.

### Compare files and identify different file types

diff is used to compare files and directories. This often-used utility program has many useful options: To compare two files, at the command prompt, type `diff [options] <filename1> <filename2>`.

Use `file <filename>` to see the type of file, e.g. bash script.

### Back up data

Basic ways to back up data include the use of simple copying with cp and use of the more robust rsync.

rsync is more efficient, because it checks if the file being copied already exists. If the file exists and there is no change in size or modification time, rsync will avoid an unnecessary copy and save time. Because rsync copies only the parts of files that have actually changed, it can be very fast.

cp can only copy files to and from destinations on the local machine, but rsync can also be used to copy files from one machine to another.

rsync is very efficient when recursively copying one directory tree to another, because only the differences are transmitted over the network. One often synchronizes the destination directory tree with the origin, using the -r option to recursively walk down the directory tree copying all files and directories below the one listed as the source.

rsync is a very powerful utility. For example, a very useful way to back up a project directory might be to use the following command: `rsync -r project-X archive-machine:archives/project-X`

Note that rsync can be very destructive! Accidental misuse can do a lot of harm to data and programs, by inadvertently copying changes to where they are not wanted. Take care to specify the correct options and paths. It is highly recommended that you first test your rsync command using the -dry-run option to ensure that it provides the results that you want.

To use rsync at the command prompt, type rsync sourcefile destinationfile; The contents of sourcefile will be copied to destinationfile.

A good combination of options is shown in: `rsync --progress -avrxH --delete sourcedir destdir`

### Compress data

File data is often compressed to save disk space and reduce the time it takes to transmit files over networks.

Linux uses a number of methods to perform this compression, including:

- gzip: The most frequently used Linux compression utility
- bzip2: Produces files significantly smaller than those produced by gzip
- xz: The most space-efficient compression utility used in Linux
- zip: Is often required to examine and decompress archives from other operating systems

These techniques vary in the efficiency of the compression and in how long they take to compress; generally, the more efficient techniques take longer. Decompression time does not vary as much across different methods.

#### gzip

gzip is the most often used Linux compression utility. It compresses very well and is very fast. The following table provides some usage examples:

- gzip \*: each file is compressed and renamed with a .gz extension
- gzip -r projectX: compresses all files in the projectX directory, along with all files in all of the directories under projectX
- gunzip foo: de-compresses foo found in the file foo.gz

#### bzip2

bzip2 has a syntax that is similar to gzip but it uses a different compression algorithm and produces significantly smaller files, at the price of taking a longer time to do its work. Thus, it is more likely to be used to compress larger files.

- bzip2 \*: compresses all of the files in the current directory and replaces each file with a file renamed with a .bz2 extension
- bunzip2 \*.bz2: decompresses all of the files with an extension of .bz2 in the current directory

#### xz

xz is the most space efficient compression utility used in Linux and is now used to store archives of the Linux kernel. Once again, it trades a slower compression speed for an even higher compression ratio.

- xz \*: compresses all of the files in the current directory and replaces each file with one with a .xz extension
- xz foo: compresses the file foo into foo.xz using the default compression level (-6), and removes foo if compression succeeds
- xz -dk bar.xz: decompresses bar.xz into bar and does not remove bar.xz even if decompression is successful
- xz -d \*.xz: decompresses the files compressed using xz

#### zip

The zip program is not often used to compress files in Linux, but is often required to examine and decompress archives from other operating systems. It is only used in Linux when you get a zipped file from a Windows user.

- zip backup \*: compresses all files in the current directory and places them in the file backup.zip
- zip -r backup.zip ~: archives your login directory (~) and all files and directories under it in the file backup.zip
- unzip backup.zip: extracts all files in the file backup.zip and places them in the current directory

#### tar

It allows you to create or extract files from an archive file, often called a tarball. At the same time, you can optionally compress while creating the archive, and decompress while extracting its contents.

- tar xvf mydir.tar: extract all the files in mydir.tar into the mydir directory
- tar zcvf mydir.tar.gz mydir: create the archive and compress with gzip
- tar jcvf mydir.tar.bz2 mydir: create the archive and compress with bz2
- tar Jcvf mydir.tar.xz mydir: create the archive and compress with xz

## Chapter 11: Text Editors

At some point, you will need to manually edit text files. You might be composing an email off-line, writing a script to be used for bash or altering a system or application configuration file.

Note that word processing applications including those that are part of office suites are not really basic text editors because they add a lot of extra (usually invisible) formatting information that will probably render system administration configuration files unusable for their intended purpose. So, using text editors really is essential in Linux.

When it comes to text editors, there are many choices, ranging from quite simple to very complex, including: nano, gedit, vi, emacs.

### How to create and edit files using the available Linux text editors

Sometimes, you may want to create a short file and don't want to bother invoking a full text editor. In addition, doing so can be quite useful when used from within scripts, even when creating longer files.

If you want to create a file without using an editor, there is an easy way to create one from the command line and fill it with content.

```
$ echo line one > myfile
$ echo line two >> myfile
$ echo line three >> myfile
```

Note that while a single greater-than sign (>) will send the output of a command to a file, two of them (>>) will append the new output to an existing file.

### nano, a simple text-based editor

Just invoke nano by giving a file name as an argument. All the help you need is displayed at the bottom of the screen, and you should be able to proceed without any problem.

nano is easy to use, and requires very little effort to learn. To open a file in nano, type `nano <filename>` and press Enter. If the file does not exist, it will be created.

nano provides a two line “shortcut bar” at the bottom of the screen that lists the available commands. Some of these commands are:

```
CTRL-G: Display the help screen
CTRL-O: Write to a file
CTRL-X: Exit a file
CTRL-R: Insert contents from another file to the current buffer
CTRL-C: Cancels previous commands
```

### gedit, a simple graphical editor

gedit is a simple-to-use graphical editor that can only be run within a Graphical Desktop environment. It is visually quite similar to the Notepad text editor in Windows, but is actually far more capable and very configurable and has a wealth of plugins available to extend its capabilities further.

To open a new file in gedit, find the program in your desktop's menu system, or from the command line type `gedit <filename>`. If the file does not exist, it will be created.

### vi and emacs, two advanced editors with both text-based and graphical interfaces

Developers and administrators experienced in working on UNIX-like systems almost always use one of the two venerable editing options: vi and emacs. Both are present or easily available on all distributions and are completely compatible with the versions available on other operating systems.

Both vi and emacs have a basic purely text-based form that can run in a non-graphical environment. They also have one or more graphical interface forms with extended capabilities; these may be friendlier for a less experienced user. While vi and emacs can have significantly steep learning curves for new users, they are extremely efficient when one has learned how to use them.

Use `vimtutor` to learn it.

vi provides three modes. It is vital to not lose track of which mode you are in. Many keystrokes and commands behave quite differently in different modes.

Command: By default, vi starts in Command mode. Each key is an editor command. Keyboard strokes are interpreted as commands that can modify file contents.

Insert: Type i to switch to Insert mode from Command mode. Insert mode is used to enter (insert) text into a file. Insert mode is indicated by an “? INSERT ?” indicator at the bottom of the screen. Press Esc to exit Insert mode and return to Command mode.

Line: Type : to switch to the Line mode from Command mode. Each key is an external command, including operations such as writing the file contents to disk or exiting. Uses line editing commands inherited from older line editors. Some line editing commands are very powerful. Press Esc to exit Line mode and return to Command mode.

```
vi myfile: start the vi editor and edit the myfile file
:w : write to the file
:x : exit vi and write out modified file
:q : quit vi
/pattern: search forward for pattern
?pattern: search backward for pattern
```

## Chapter 12: User Environment

### Use and configure user accounts and user groups

To identify the current user, type `whoami`.

Most commonly, users only fiddle with ~/.bashrc, as it is invoked every time a new command line shell initiates, or another program is launched from a terminal window, while the other files are read and executed only when the user first logs onto the system.

You can create customized commands or modify the behavior of already existing ones by creating aliases. Most often, these aliases are placed in your ~/.bashrc file so they are available to any command shells you create. unalias removes an alias.

Typing alias with no arguments will list currently defined aliases.

Please note there should not be any spaces on either side of the equal sign and the alias definition needs to be placed within either single or double quotes if it contains any spaces.

Distributions have straightforward graphical interfaces for creating and removing users and groups and manipulating group membership. However, it is often useful to do it from the command line or from within shell scripts. Only the root user can add and remove users and groups.

Adding a new user is done with useradd and removing an existing user is done with userdel. In the simplest form, an account for the new user bjmoose would be done with: `sudo useradd bjmoose`.

Adding a user to an already existing group is done with usermod. For example, you would first look at what groups the user already belongs to: `groups rjsquirrel` `bjmoose : rjsquirrel`.

The root account is very powerful and has full access to the system. Other operating systems often call this the administrator account; in Linux, it is often called the superuser account. You must be extremely cautious before granting full root access to a user. External attacks often consist of tricks used to elevate to the root account.

When assigning elevated privileges, you can use the command su to launch a new shell running as another user. Most often, this other user is root, and the new shell allows the use of elevated privileges until it is exited. It is almost always a bad practice to use su to become root. Granting privileges using sudo is less dangerous and is preferred. By default, sudo must be enabled on a per-user basis.

Typing long commands and filenames over and over gain gets rather tedious, and leads to a lot of trivial errors, such as typos. Deploying aliases allows us to define shortcuts to alleviate the pain of all of this typing.

### Use and set environment variables

Environment variables are quantities that have specific values which may be utilized by the command shell, such as bash, or other utilities and applications. Some environment variables are given preset values by the system (which can usually be overridden), while others are set directly by the user, either at the command line or within startup and other scripts.

An environment variable is actually just a character string that contains information used by one or more applications. There are a number of ways to view the values of currently set environment variables; one can type set, env, or export. Depending on the state of your system, set may print out many more lines than the other two methods.

### Use the previous shell command history

`history` to see history
`!<number>` to rerun it

### Use and define aliases

`alias newName="cd /path"`

### Use and set file permissions and ownership

In Linux, every file is associated with a user who is the owner. Every file is also associated with a group which has an interest in the file and certain rights, or permissions: read, write, and execute.

The following utility programs involve user and group ownership and permission setting:
chown: Used to change user ownership of a file or directory
chgrp: Used to change group ownership
chmod: Used to change the permissions on the file, which can be done separately for owner, group and the rest of the world

#### chmod

Files have three kinds of permissions: read (r), write (w), execute (x). These are generally represented as in rwx. These permissions affect three groups of owners: user/owner (u), group (g), and others (o).

There are a number of different ways to use chmod. For instance, to give the owner and others execute permission and remove the group write permission:

One often uses a shorthand which lets you set all the permissions in one step. This is done with a simple algorithm, and a single digit suffices to specify all three permission bits for each entity. This digit is the sum of:

4 if read permission is desired, 2 if write permission is desired, 1 if execute permission is desired. Thus, 7 means read/write/execute, 6 means read/write, and 5 means read/execute.

## Chapter 13 : Manipulating Text

- cat is used to read, print, and combine files.
- echo displays a line of text either on standard output or to place in a file.
- sed is used to filter and perform substitutions on files and text data streams.
- awk is used as a data extraction and reporting tool.
- sort is used to sort text files and output streams in either ascending or descending order.
- uniq eliminates duplicate entries in a text file.
- paste combines fields from different files. It can also extract and combine lines from multiple sources.
- join combines lines from two files based on a common field.
- split breaks up a large file into equal-sized segments.
- Regular expressions are text strings used for pattern matching.
- grep searches text files and data streams for patterns and can be used with regular expressions.
- tr translates characters, copies standard input to standard output, and handles special characters.
- tee saves a copy of standard output to a file while still displaying at the terminal
- wc (word count) displays the number of lines, words, and characters in a file or group of files.
- cut extracts columns from a file.
- less views files a page at a time and allows scrolling in both directions.
- head displays the first few lines of a file or data stream on standard output.
- tail displays the last few lines of a file or data stream on standard output.
- strings extracts printable character strings from binary files.
- The z command family is used to read and work with compressed files.

### Display and append to file contents using cat and echo

Irrespective of the role you play with Linux (system administrator, developer or user), you often need to browse through and parse text files, and/or extract data from them. These are file manipulation operations. Thus, it is essential for the Linux user to become adept at performing certain operations on files.

Most of the time, such file manipulation is done at the command line, which allows users to perform tasks more efficiently than while using a GUI. Furthermore, the command line is more suitable for automating often executed tasks.

Indeed, experienced system administrators write customized scripts to accomplish such repetitive tasks, standardized for each particular environment. We will discuss such scripting later in much detail.

#### cat

cat is short for concatenate and is one of the most frequently used Linux command line utilities. It is often used to read and print files, as well as for simply viewing file contents. To view a file, use the following command: `cat <filename>`

For example, `cat readme.txt` will display the contents of readme.txt on the terminal. However, the main purpose of cat is often to concatenate multiple files together.

The tac command (cat spelled backwards) prints the lines of a file in reverse order. Each line remains the same, but the order of lines is inverted. The syntax of tac is exactly the same as for cat, as in: `tac file`

```
cat file1 file2: concatenate multiple files and display the output
cat file1 file2 > newfile: combine multiple files and save the output into a new file
cat file >> existingfile: append a file to the end of an existing file
```

#### echo

echo simply displays (echoes) text: `echo string`

echo can be used to display a string on standard output (i.e. the terminal) or to place in a new file (using the > operator) or append to an already existing file (using the >> operator).

echo is particularly useful for viewing the values of environment variables (built-in shell variables). For example, echo \$USERNAME will print the name of the user who has logged into the current terminal.

#### less

System administrators need to work with configuration files, text files, documentation files, and log files. Some of these files may be large or become quite large as they accumulate data with time.

In such cases, directly opening the file in an editor will cause issues, due to high memory utilization, as an editor will usually try to read the whole file into memory first. However, one can use less to view the contents of such a large file, scrolling up and down page by page, without the system having to place the entire file in memory before starting. This is much faster than using a text editor.

Viewing somefile can be done by typing either of the two following commands: `less somefile`, `cat somefile | less`

#### sed

sed is a powerful text processing tool. It is used to modify the contents of a file, usually placing the contents into a new file. Its name is an abbreviation for stream editor. sed can filter text, as well as perform substitutions in data streams.

Data from an input source/file (or stream) is taken and moved to a working space. The entire list of operations/modifications is applied over the data in the working space and the final contents are moved to the standard output space (or stream).

#### awk

awk is used to extract and then print specific contents of a file and is often used to construct reports. It is a powerful utility and interpreted programming language. It is used to manipulate data files, retrieving, and processing text. It works well with fields (containing a single piece of data, essentially a column) and records (a collection of fields, essentially a line in a file).

#### File Manipulation

In managing your files, you may need to perform many tasks, such as sorting data and copying data from one location to another. Linux provides several file manipulation utilities that you can use while working with text files: sort, uniq, paste, join, split.

#### grep

grep is extensively used as a primary text searching tool. It scans files for specified patterns and can be used with regular expressions, as well as simple strings.

## Chapter 14: Network Operations

### Explain basic networking concepts, including types of networks and addressing issues

A network is a group of computers and computing devices connected together through communication channels, such as cables or wireless media.

A network is used to: Allow the connected devices to communicate with each other, Enable multiple users to share devices over the network, such as printers and scanners, Share and manage information across computers easily.

Most organizations have both an internal network and an Internet connection for users to communicate with machines and people outside the organization. The Internet is the largest network in the world and can be called "the network of networks".

Devices attached to a network must have at least one unique network address identifier known as the IP address. The address is essential for routing packets of information through the network.

Exchanging information across the network requires using streams of small packets, each of which contains a piece of the information going from one machine to another. These packets contain data buffers together with headers which contain information about where the packet is going to and coming from, and where it fits in the sequence of packets that constitute the stream.

There are two different types of IP addresses available: IPv4 and IPv6. IPv4 is older and by far the more widely used, while IPv6 is newer and is designed to get past limitations inherent in the older standard and furnish many more possible addresses.

IPv4 uses 32-bits for addresses; there are only 4.3 billion unique addresses available. Furthermore, many addresses are allotted and reserved, but not actually used. IPv4 is considered inadequate for meeting future needs because the number of devices available on the global network has increased enormously in recent years.

IPv6 uses 128-bits for addresses; this allows for 3.4 X 10^38 unique addresses. If you have a larger network of computers and want to add more, you may want to move to IPv6, because it provides more unique addresses.

One reason IPv4 has not disappeared is there are ways to effectively make many more addresses available by methods such as NAT. NAT enables sharing one IP address among many locally connected computers, each of which has a unique address only seen on the local network. While this is used in organizational settings, it also used in simple home networks. For example, if you have a router hooked up to your Internet Provider it gives you one externally visible address, but issues each device in your home an individual local address.

You can assign IP addresses to computers over a network either manually or dynamically. Manual assignment adds static (never changing) addresses to the network. Dynamically assigned addresses can change every time you reboot or even more often; the Dynamic Host Configuration Protocol (DHCP) is used to assign IP addresses.

Name Resolution is used to convert numerical IP address values into a human-readable format known as the hostname. For example, 104.95.85.15 is the numerical IP address that refers to the hostname whitehouse.gov. Hostnames are much easier to remember!

Given an IP address, you can obtain its corresponding hostname. Accessing the machine over the network becomes easier when you can type the hostname instead of the IP address.

The special hostname localhost is associated with the IP address 127.0.0.1, and describes the machine you are currently on (which normally has additional network-related IP addresses).

DNS (Domain Name System) is used for converting Internet domain and host names to IP addresses.

### Configure network interfaces and use basic networking utilities

Network interfaces are a connection channel between a device and a network. Physically, network interfaces can proceed through a network interface card (NIC), or can be more abstractly implemented as software. You can have multiple network interfaces operating at once.

Information about a particular network interface or all network interfaces can be reported by the ip and ifconfig utilities. ip is newer than ifconfig and has far more capabilities, but its output is uglier to the human eye.

- `ifconfig` is used to display current active network interfaces.
- `ip addr show` and `ip route show` can be used to view IP address and routing information.
- `ping` to check if the remote host is alive and responding.
- `route` to manage IP routing.
- `wget` to download webpages.
- `curl` to obtain information about URLs.

### Use graphical and non-graphical browsers

Browsers are used to retrieve, transmit, and explore information resources, usually on the World Wide Web. Linux users commonly use both graphical and non-graphical browser applications. The common graphical browsers used in Linux are: Firefox, Google Chrome.
You can also use non-graphical browsers, such as: Lynx, ELinks, w3m.

Sometimes, you need to download files and information, but a browser is not the best choice. wget is a command line utility that can capably handle this. To download a web page, you can simply type `wget <url>`, and then you can read the downloaded page as a local file using a graphical or non-graphical browser.

Besides downloading, you may want to obtain information about a URL, such as the source code being used. curl can be used from the command line or a script to read such information. curl also allows you to save the contents of a web page to a file, as does wget. You can read a URL using `curl <URL>`. To get the contents of a web page and store it to a file, type `curl -o saved.html http://www.mysite.com`.

### Transfer files to and from clients and servers

#### FTP

When you are connected to a network, you may need to transfer files from one machine to another. File Transfer Protocol (FTP) is a well-known and popular method for transferring files between computers using the Internet. This method is built on a client-server model. FTP can be used within a browser or with stand-alone client programs.

FTP is one of the oldest methods of network data transfer, dating back to the early 1970s. As such, it is considered inadequate for modern needs, as well as being intrinsically insecure. FTP has fallen into disfavor on modern systems, as it is intrinsically insecure, since passwords are user credentials that can be transmitted without encryption and are thus prone to interception. Thus, it was removed in favor of using rsync and web browser https access for example.

FTP clients enable you to transfer files with remote computers using the FTP protocol. These clients can be either graphical or command line tools.

#### SSH

Secure Shell (SSH) is a cryptographic network protocol used for secure data communication. It is also used for remote services and other secure services between two devices on the network and is very useful for administering systems which are not easily available to physically work on, but to which you have remote access.

To login to a remote system using your same user name you can just type `ssh some_system`. ssh then prompts you for the remote password. You can also configure ssh to securely allow your remote access without typing a password each time.

If you want to run as another user, you can do either `ssh -l someone some_system` or `ssh someone@some_system`. To run a command on a remote system via SSH, at the command prompt, you can type `ssh some_system my_command`.

## Chapter 15 : The Bash Shell and Basic Scripting

### Explain the features and capabilities of bash shell scripting

Suppose you want to look up a filename, check if the associated file exists, and then respond accordingly, displaying a message confirming or not confirming the file's existence. If you only need to do it once, you can just type a sequence of commands at a terminal. However, if you need to do this multiple times, automation is the way to go. In order to automate sets of commands, you will need to learn how to write shell scripts, the most common of which are used with bash.

Typing a long sequence of commands at a terminal window can be complicated, time consuming, and error prone. By deploying shell scripts, using the command line becomes an efficient and quick way to launch complex sequences of steps. The fact that shell scripts are saved in a file also makes it easy to use them to create new script variations and share standard procedures with several users.

A shell is a command line interpreter which provides the user interface for terminal windows. It can also be used to run scripts, even in non-interactive sessions without a terminal window, as if the commands were being directly typed in.

The first line of the script, that starts with `#!`, contains the full path of the command interpreter (in this case `/bin/bash`) that is to be used on the file. As we have noted, you have quite a few choices for the scripting language you can use, such as /usr/bin/perl, /bin/csh, /usr/bin/python, etc.

`read x` to save var in x
`$x` to use var
`$(<command>)` ro run command in var

Scripts are a sequence of statements and commands stored in a file that can be executed by a shell.
Command substitution allows you to substitute the result of a command as a portion of another command.
Functions or routines are a group of commands that are used for execution.
Environmental variables are quantities either preassigned by the shell or defined and modified by the user.
To make environment variables visible to child processes, they need to be exported.
Scripts can behave differently based on the parameters (values) passed to them.
The process of writing the output to a file is called output redirection.
The process of reading input from a file is called input redirection.
The if statement is used to select an action based on a condition.

## Chapter 16: More on Bash Shell Scripting

You can manipulate strings to perform actions such as comparison, sorting, and finding length.
You can use Boolean expressions when working with multiple data types, including strings or numbers, as well as files.
The output of a Boolean expression is either true or false.
Operators used in Boolean expressions include the && (AND), ||(OR), and ! (NOT) operators.
We looked at the advantages of using the case statement in scenarios where the value of a variable can lead to different execution paths.
Script debugging methods help troubleshoot and resolve errors.
The standard and error outputs from a script or shell commands can easily be redirected into the same file or separate files to aid in debugging and saving results
Linux allows you to create temporary files and directories, which store data for a short duration, both saving space and increasing security.
Linux provides several different ways of generating random numbers, which are widely used.

## Chapter 17: Printing

### Configure a printer on a Linux machine

To manage printers and print directly from a computer or across a networked environment, you need to know how to configure and install a printer. Printing itself requires software that converts information from the application you are using to a language your printer can understand. The Linux standard for printing software is the Common UNIX Printing System (CUPS).

Modern Linux desktop systems make installing and administering printers pretty simple and intuitive, and not unlike how it is done on other operating systems.

#### CUPS Overview

CUPS is the underlying software almost all Linux systems use to print from applications like a web browser or LibreOffice. It converts page descriptions produced by your application and then sends the information to the printer. It acts as a print server for both local and network printers.

Printers manufactured by different companies may use their own particular print languages and formats. CUPS uses a modular printing system which accommodates a wide variety of printers and also processes various data formats. This makes the printing process simpler; you can concentrate more on printing and less on how to print.

Generally, the only time you should need to configure your printer is when you use it for the first time. In fact, CUPS often figures things out on its own by detecting and configuring any printers it locates.

CUPS carries out the printing process with the help of its various components: Configuration Files, Scheduler, Job Files, Log Files, Filter, Printer Drivers, Backend.

Scheduler: CUPS is designed around a print scheduler that manages print jobs, handles administrative commands, allows users to query the printer status, and manages the flow of data through all CUPS components. We will look at the browser-based interface that can be used with CUPS, which allows you to view and manipulate the order and status of pending print jobs.

Configuration Files: The print scheduler reads server settings from several configuration files, the two most important of which are cupsd.conf and printers.conf. These and all other CUPS related configuration files are stored under the /etc/cups/ directory. cupsd.conf is where most system-wide settings are located; it does not contain any printer-specific details. Most of the settings available in this file relate to network security, i.e. which systems can access CUPS network capabilities, how printers are advertised on the local network, what management features are offered, and so on. printers.conf is where you will find the printer-specific settings. For every printer connected to the system, a corresponding section describes the printer’s status and capabilities. This file is generated only after adding a printer to the system and should not be modified by hand.

Job Files: CUPS stores print requests as files under the /var/spool/cups directory (these can actually be accessed before a document is sent to a printer). Data files are prefixed with the letter "d" while control files are prefixed with the letter "c". After a printer successfully handles a job, data files are automatically removed. These data files belong to what is commonly known as the print queue.

Log Files: Log files are placed in /var/log/cups and are used by the scheduler to record activities that have taken place. These files include access, error, and page records. Note on some distributions permissions are set such that you don't need the sudo. You can view the log files with the usual tools.

Filters, Printer Drivers, and Backends: CUPS uses filters to convert job file formats to printable formats. Printer drivers contain descriptions for currently connected and configured printers, and are usually stored under /etc/cups/ppd/. The print data is then sent to the printer through a filter and via a backend that helps to locate devices connected to the system. So, in short, when you execute a print command, the scheduler validates the command and processes the print job, creating job files according to the settings specified in the configuration files. Simultaneously, the scheduler records activities in the log files. Job files are processed with the help of the filter, printer driver, and backend, and then sent to the printer.

Managing CUPS: Assuming CUPS has been installed you'll need to start and manage the CUPS daemon so that CUPS is ready for configuring a printer. Managing the CUPS daemon is simple; all management features can be done with the systemctl utility.

### Manipulate postscript and PDF files using command line utilities

PostScript is a standard page description language. It effectively manages scaling of fonts and vector graphics to provide quality printouts. It is purely a text format that contains the data fed to a PostScript interpreter. The format itself is a language that was developed by Adobe in the early 1980s to enable the transfer of data to printers.

Postscript has been for the most part superseded by the PDF format which produces far smaller files in a compressed format for which support has been integrated into many applications. However, one still has to deal with postscript documents, often as an intermediate format on the way to producing final documents.

CUPS provides two command-line interfaces: the System V and BSD.
The CUPS interface is available at http://localhost:631.
lp and lpr are used to submit a document to CUPS directly from the command line.
lpoptions can be used to set printer options and defaults.
PostScript effectively manages scaling of fonts and vector graphics to provide quality prints.
enscript is used to convert a text file to PostScript and other formats.
Portable Document Format (PDF) is the standard format used to exchange documents while ensuring a certain level of consistency in the way the documents are viewed.
pdftk joins and splits PDFs; pulls single pages from a file; encrypts and decrypts PDF files; adds, updates, and exports a PDF’s metadata; exports bookmarks to a text file; adds or removes attachments to a PDF; fixes a damaged PDF; and fills out PDF forms.
pdfinfo can extract information about PDF documents.
flpsed can add data to a PostScript document.
pdfmod is a simple application with a graphical interface that you can use to modify PDF documents.

## Chapter 18: Local Security Principles

### Best practices and tools for making Linux systems as secure as possible

User Accounts: The Linux kernel allows properly authenticated users to access files and applications. While each user is identified by a unique integer (the user id or UID), a separate database associates a username with each UID. Upon account creation, new user information is added to the user database and the user's home directory must be created and populated with some essential files. Command line programs such as useradd and userdel as well as GUI tools are used for creating and removing accounts.

Types of Accounts: By default, Linux distinguishes between several account types in order to isolate processes and workloads. Linux has four types of accounts: root, system, Normal, Network.

For a safe working environment, it is advised to grant the minimum privileges possible and necessary to accounts, and remove inactive accounts. The last utility, which shows the last time each user logged into the system, can be used to help identify potentially inactive accounts which are candidates for system removal.

Keep in mind that practices you use on multi-user business systems are more strict than practices you can use on personal desktop systems that only affect the casual user. This is especially true with security. We hope to show you practices applicable to enterprise servers that you can use on all systems, but understand that you may choose to relax these rules on your own personal system.

root is the most privileged account on a Linux/UNIX system. This account has the ability to carry out all facets of system administration, including adding accounts, changing user passwords, examining log files, installing software, etc. Utmost care must be taken when using this account. It has no security restrictions imposed upon it.

root privileges are required to perform operations such as: Creating, removing and managing user accounts; Managing software packages; Removing or modifying system files; Restarting system services.

Regular account users of Linux distributions might be allowed to install software packages, update some settings, use some peripheral devices, and apply various kinds of changes to the system. However, root privilege is required for performing administration tasks such as restarting services, manually installing packages and managing parts of the filesystem that are outside the normal user’s directories.

In Linux you can use either su or sudo to temporarily grant root access to a normal user; these methods are actually quite different.

### Explain the importance of process isolation and hardware access

Process Isolation: Linux is considered to be more secure than many other operating systems because processes are naturally isolated from each other. One process normally cannot access the resources of another process, even when that process is running with the same user privileges. Linux thus makes it difficult (though certainly not impossible) for viruses and security exploits to access and attack random resources on a system.

Hardware Device Access: Linux limits user access to non-networking hardware devices in a manner that is extremely similar to regular file access. Applications interact by engaging the filesystem layer (which is independent of the actual device or hardware the file resides on). This layer will then open a device special file (often called a device node) under the /dev directory that corresponds to the device being accessed. Each device special file has standard owner, group and world permission fields. Security is naturally enforced just as it is when standard files are accessed.

Keeping Current: When security problems in either the Linux kernel or applications and libraries are discovered, Linux distributions have a good record of reacting quickly and pushing out fixes to all systems by updating their software repositories and sending notifications to update immediately. The same thing is true with bug fixes and performance improvements that are not security related.

### Work with passwords, including how to set and change them

The SHA-512 algorithm is typically used to encode passwords. They can be encrypted, but not decrypted.

Pluggable Authentication Modules (PAM) can be configured to automatically verify that passwords created or modified using the passwd utility are strong enough (what is considered strong enough can also be configured).

### Describe how to secure the boot process and hardware resources

Hardware Vulnerability: When hardware is physically accessible, security can be compromised by: Key logging, Recording the real time activity of a computer user including the keys they press. The captured data can either be stored locally or transmitted to remote machines. Network sniffing, Capturing and viewing the network packet level data on your network, ooting with a live or rescue disk, Remounting and modifying disk content.

Your IT security policy should start with requirements on how to properly secure physical access to servers and workstations. Physical access to a system makes it possible for attackers to easily leverage several attack vectors, in a way that makes all operating system level recommendations irrelevant.

The guidelines of security are: Lock down workstations and servers. Protect your network links such that it cannot be accessed by people you do not trust. Protect your keyboards where passwords are entered to ensure the keyboards cannot be tampered with. Ensure a password protects the BIOS in such a way that the system cannot be booted with a live or rescue DVD or USB key.
