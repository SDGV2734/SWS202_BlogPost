---
title: Files Description and Redirection 
slug: File_Descriptors_and_Redirections
description: What file description and how to redirect to them 
image: ../images/snippets/File_Descriptors_and_Redirections.webp
---
## File Descriptors and Redirections

### What is a File Descriptor (FD)?

- A file descriptor (FD) in Unix/Linux is a reference, maintained by the kernel, to manage Input/Output (I/O) operations.
- It acts as a unique identifier for open files, sockets, or other I/O resources.
- In Windows, this concept is known as a **file handle**.
- Think of it as a **coatroom ticket**: the ticket (FD) represents your access to a resource (like a file), and the system uses it to locate and manage the resource.

### Standard File Descriptors

By default, the first three FDs are:

1. **STDIN (Standard Input)** – FD 0
2. **STDOUT (Standard Output)** – FD 1
3. **STDERR (Standard Error)** – FD 2

### Examples

#### STDIN and STDOUT with `cat`

```bash
$ cat
SOME INPUT
SOME INPUT  # echoed as STDOUT

```

#### STDOUT and STDERR with `find`

```bash
$ find /etc/ -name shadow
# Permission denied (STDERR)

```

#### Redirect STDERR to Null

```bash
$ find /etc/ -name shadow 2>/dev/null

```

#### Redirect STDOUT to a File

```bash
$ find /etc/ -name shadow 2>/dev/null > results.txt

```

#### Redirect STDOUT and STDERR to Separate Files

```bash
$ find /etc/ -name shadow 2> stderr.txt 1> stdout.txt

```

#### Redirect STDIN from a File

```bash
$ cat < stdout.txt

```

#### Append STDOUT to an Existing File

```bash
$ find /etc/ -name passwd >> stdout.txt 2>/dev/null

```

#### Use Here-Document to Redirect STDIN Stream

```bash
$ cat << EOF > stream.txt
Some streaming input
EOF

```

#### Use Pipes to Chain Commands

```bash
$ find /etc/ -name *.conf 2>/dev/null | grep systemd

```

#### Pipe Output and Count Results

```bash
$ find /etc/ -name *.conf 2>/dev/null | grep systemd | wc -l

```

### Summary

- Understanding FDs and redirection allows us to efficiently manage I/O operations.
- We can manipulate input and output using redirections (`>`, `>>`, `<`, `<<`) and pipes (`|`).
- These tools help us streamline processes, manage data flow, and improve productivity.

A file descriptor (FD) in Unix/Linux operating systems is a reference, maintained by the kernel, that allows the system to manage Input/Output (I/O) operations. It acts as a unique identifier for an open file, socket, or any other I/O resource. In Windows-based operating systems, this is known as a file handle. Essentially, the file descriptor is the system's way of keeping track of active I/O connections, such as reading from or writing to a file.

Think of it as a ticket number you get when checking in your coat at a coatroom. The ticket (file descriptor) represents your connection to your coat (file or resource), and whenever you need to retrieve your coat (perform I/O), you present the ticket to the attendant (operating system) who knows exactly where your coat is stored (which resource the file descriptor refers to). Without the ticket, you'd have no way of efficiently accessing your coat among the many others stored, just as without a file descriptor, the operating system wouldn't know which resource to interact with. You will soon see why file descriptors are so
important and why understanding them is crucial as we dive into the upcoming examples.

By default, the first three file descriptors in Linux are:

1. Data Stream for Input
STDIN – 0
2. Data Stream for Output
STDOUT – 1
3. Data Stream for Output that relates to an error occurring.
STDERR – 2

#### STDIN and STDOUT

Let us see an example with cat. When running cat, we give the running program our standard input (STDIN - FD 0),  wherein this case "SOME INPUT" is. As soon as we have confirmed our input with [ENTER], it is returned to the terminal as standard output (STDOUT - FD 1), marked red.