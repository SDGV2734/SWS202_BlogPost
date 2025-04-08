---
title: Linux Structure 
slug: encode-files
description: Understanding Linux Structure
image: ../images/snippets/Linux_structure/LinuxStructure.png
---

## Linux structure

Linux, as you might already know, is an operating system used for personal computers, servers, and even mobile devices. However, Linux stands as a fundamental pillar in cybersecurity, renowned for its robustness, flexibility, and open-source nature. In this section we are going to cover the Linux structure, history, philosophy, architecture, and file system hierarchy— essential knowledge for any cybersecurity professional. You can think of this as your first driving lesson for a new car, getting a basic understanding of the vehicle, what it consists of, and why it is the way it currently is. 

To begin, let's define what Linux is. Linux is an operating system, just like Windows, macOS, iOS, or Android. An operating system (OS) is software that manages all the hardware resources of a computer, facilitating communication between software applications and hardware components. Unlike some other operating systems, Linux comes in many different distributions—
often called "distros"—which are versions of Linux tailored to various needs and preferences.

## History

Many events led up to creating the first Linux kernel and, ultimately, the Linux operating system (OS), starting with the Unix operating system's release by Ken Thompson and Dennis Ritchie (whom both worked for AT&T at the time) in 1970. The Berkeley Software Distribution (BSD) was released in 1977, but since it contained the Unix code owned by AT&T, a resulting lawsuit limited the development of BSD. Richard Stallman started the GNU project in 1983. His goal was to create a free Unix-like operating system, and part of his work resulted in the GNU General Public License (GPL) being created. Projects by others over the years failed to result in a working, free kernel that would become widely adopted until the creation of the Linux kernel.

At first, Linux was a personal project started in 1991 by a Finnish student named Linus Torvalds. His goal was to create a new, free operating system kernel. Over the years, the Linux kernel has gone from a small number of files written in C under licensing that prohibited commercial distribution to the latest version with over 23 million source code lines (comments excluded), licensed under the GNU General Public License v2.

Linux is available in over 600 distributions (or an operating system based on the Linux kernel and supporting software and libraries). Some of the most popular and well-known being Ubuntu, Debian, Fedora, OpenSUSE, elementary, Manjaro, Gentoo Linux, RedHat, and Linux Mint.

Linux is generally considered more secure than other operating systems, and while it has had many kernel vulnerabilities in the past, it is becoming less and less frequent. It is less susceptible to malware than Windows operating systems and is very frequently updated. Linux is also very stable and generally affords very high performance to the end-user. However, it can be more difficult for beginners and does not have as many hardware drivers as Windows.

Since Linux is free and open-source, the source code can be modified and distributed commercially or non-commercially by anyone. Linux-based operating systems run on servers, mainframes, desktops, embedded systems such as routers, televisions, video game consoles, and more. The overall Android operating system that runs on smartphones and tablets is based on the Linux kernel, and because of this, Linux is the most widely installed operating system.

Linux is an operating system like Windows, iOS, Android, or macOS. An OS is software that manages all of the hardware resources associated with our computer. That means that an OS manages the whole communication between software and hardware. Also, there exist many different distributions (distro). It is like a version of Windows operating systems. With the interactive instances, we get access to the Pwnbox, a customized version of Parrot OS. This will be the primary OS we will work with through the modules. Parrot OS is a Debian-based Linux distribution that focuses on security, privacy, and development.

Imagine Linux as a thriving company where its components are the dedicated employees, each with specific roles and responsibilities to keep operations running smoothly. The architecture serves as the organizational structure, outlining how these employees are arranged into departments and how they communicate to achieve efficiency and productivity. The philosophy represents the company's culture and core values, guiding how these employees work individually and collaboratively, promoting principles like simplicity, transparency, and cooperation to reach common goals.

## Philosophy

The Linux philosophy centers on simplicity, modularity, and openness. It advocates for building small, single-purpose programs that perform one task well. These programs can be combined in various ways to accomplish complex operations, promoting efficiency and flexibility. Linux follows five core principles:

![image.png](../images/snippets/Linux_structure/image.png)

## Components

![image.png](../images/snippets/Linux_structure/image_1.png)

![image.png](../images/snippets/Linux_structure/image_2.png)

## Linux Architecture

![image.png](../images/snippets/Linux_structure/image_3.png)

## File System Hierarchy

The Linux operating system is structured in a tree-like hierarchy and is documented in the [Filesystem Hierarchy](https://www.pathname.com/fhs/) Standard FHS). Linux is structured with the following standard top-level directories:

![image.png](../images/snippets/Linux_structure/image_4.png)