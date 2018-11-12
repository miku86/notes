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

## Chapter 12: User Environment

## Chapter 13 : Manipulating Text

## Chapter 14: Network Operations

## Chapter 15 : The Bash Shell and Basic Scripting

## Chapter 16: More on Bash Shell Scripting

## Chapter 17: Printing

## Chapter 18: Local Security Principles
