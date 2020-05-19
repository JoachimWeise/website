---
title: Getting Started with WSL
subtitle: Windows Subsystem for Linux
date: 2020-02-18
# lastmod: 2020-01-21
bigimg: [{src: "/img/2020-02-18-wsl-getting-started.jpg", desc: "Leipzig Museum der Bildenden Künste (2019)"}]
tags: ["linux"]
---

The Windows Subsystem for Linux (WSL) is a great solution for developers to natively work within Linux right on their Windows 10 version desktop. WSL lets developers run a GNU/Linux environment -- including most command-line tools, utilities, and applications -- directly on Windows, unmodified, without the overhead of a virtual machine. After some surprisingly super-easy setup, this gives you a truly native POSIX / Unix-like environment directly integrated into your Windows PC, essentially negating a vast majority of issues people had previously with workarounds like dual booting, VMing or terminal wrappers like CYGWIN or Git Bash. According to [Microsoft](https://docs.microsoft.com/en-us/windows/wsl/faq), WSL requires fewer resources (CPU, memory, and storage) than a full virtual machine while also allowing users to use Windows apps and Linux tools on the same set of files. In this article I'm covering some background on WSL and show how to get started.
 
<!--more-->

[NOTE: THIS IS WORK IN PROGRESS]


## Motivation

[POSIX](https://en.wikipedia.org/wiki/POSIX), the Portable Operating System Interface, is a family of standards specified by the IEEE Computer Society for maintaining compatibility between operating systems. POSIX defines the application programming interface (API), along with command line shells and utility interfaces, for software compatibility with variants of Unix and other operating systems. Mac and Linux are considered to be POSIX, but Windows is not, and this makes it difficult for some developers, especially webdevs, to develop on Windows as they need access to a POSIX environment.

The Windows Subsystem for Linux overcomes this limitation by allowing developers to access a fully integrated, native Linux environment that is directly mounted to their Windows OS. This means Developers no longer have to Dual boot or use console wrappers like CYGWIN or Git Bash. They have a Linux Subsystem that is fully capable of running Linux Shell commands and POSIX Software on their Windows files.

As documented by [Wikipedia](https://en.wikipedia.org/wiki/Windows_Subsystem_for_Linux#Development),   Microsoft's first foray into achieving Unix-like compatibility on Windows began with the Microsoft POSIX Subsystem, superseded by Windows Services for UNIX via MKS/Interix, which was eventually deprecated with the release of Windows 8.1. The technology behind Windows Subsystem for Linux originated in the unreleased Project Astoria, which enabled some Android applications to run on Windows 10 Mobile.

## WSL 1 

Whereas Microsoft's previous projects had focused on creating their own unique Unix-like environments based on the POSIX standard, WSL aims for native Linux compatibility. Instead of wrapping non-native functionality into Win32 system calls as these prior systems utilized, WSL's initial design (WSL 1) leveraged the NT kernel executive to serve Linux programs as special, isolated minimal processes (known as "pico processes") attached to kernel mode "pico providers" as dedicated system call and exception handlers distinct from that of a vanilla NT process, opting to reutilize existing NT implementations wherever possible.

Since its inception, Microsoft Windows NT was designed to allow environment subsystems like Win32 to present a programmatic interface to applications without being tied to implementation details inside the kernel. This enabled the NT kernel to support POSIX, OS/2 and Win32 subsystems at its initial release. While, over time, the initial subsystems were retired, the ability of the Windows NT Kernel to allow new subsystem environments [provided Microsoft with the opportunity](https://blogs.msdn.microsoft.com/wsl/2016/04/22/windows-subsystem-for-linux-overview/) to re-use the initial investments made in this area and broaden them to develop the Windows Subsystem for Linux.

WSL 1 executes unmodified Linux ELF64 binaries by virtualizing a Linux kernel interface on top of the Windows NT kernel.  One of the kernel interfaces that it exposes are system calls (syscalls). A system call is the programmatic way in which a computer program requests a service from the kernel of the operating system it is executed on. This may include hardware-related services (for example, accessing a hard disk drive), creation and execution of new processes, and communication with integral kernel services such as process scheduling. System calls provide an essential interface between a process and the operating system. Both the Linux kernel and Windows NT kernel expose several hundred syscalls to user mode, but they have different semantics and are generally not directly compatible. For example, the Linux kernel includes things like fork, open, and kill while the Windows NT kernel has the comparable NtCreateProcess, NtOpenFile, and NtTerminateProcess.

WSL 1 features no hardware emulation/virtualization and makes direct use of the host file system and some parts of the hardware, such as the network. Web servers for example, can be accessed through the same interfaces and IP addresses configured on the host, which guarantees interoperability. There are certain locations (such as system folders) and configurations whose access/modification is restricted, even when running as root, with `sudo` from the shell. Microsoft states that WSL 1 was primarily designed for the development of applications, although in benchmarks the performance of WSL 1 is often near native Linux Ubuntu or Debian.

## WSL 2

## Installing WSL 1


## Desktop Environment

## Windows Terminal 


## Sources:

* [WSL documentation](https://docs.microsoft.com/en-us/windows/wsl/about) by Microsoft
* Windows Subsystem for Linux [Overview](https://blogs.msdn.microsoft.com/wsl/2016/04/22/windows-subsystem-for-linux-overview/)
* [Get started](https://docs.microsoft.com/en-us/learn/modules/get-started-with-windows-subsystem-for-linux/) with the Windows Subsystem for Linux
* [Windows Subsystem for Linux Setup](https://github.com/michaeltreat/Windows-Subsystem-For-Linux-Setup-Guide)
* Windows Subsystem for Linux (WSL): [The Ultimate Guide](https://adamtheautomator.com/windows-subsystem-for-linux/)
* Run [Hyper-V](https://www.tenforums.com/tutorials/139405-run-hyper-v-virtualbox-vmware-same-computer.html), VirtualBox and VMware on same Computer
* Linux on Windows: WSL with [Desktop Environment](https://dev.to/darksmile92/linux-on-windows-wsl-with-desktop-environment-via-rdp-522g) via RDP
* Windows Subsystem for Linux - Add [desktop experience](https://www.tenforums.com/tutorials/144208-windows-subsystem-linux-add-desktop-experience-ubuntu.html) to Ubuntu
* Microsoft [Terminal](https://github.com/microsoft/terminal) repo on github
