---
title: System Information 
slug: system_information
description: Learning about the system before doing anything 
image: ../images/snippets/InformationSystem.webp
---


Now, let’s dive into some hands-on practice to get comfortable with using the terminal and the shell. Keep in mind that you can
always use the -h, --help, or man commands to access help if needed.

Since we’ll be working with various Linux systems, it's important to understand their structure, including system details, processes, network configurations, users/user settings, and directories, along with their related parameters. Below is a list of essential tools to help gather this information. Most of these tools come pre-installed. However, this knowledge is not only crucial for routine Linux tasks, but also plays a key role when assessing security configurations, identifying vulnerabilities, or preventing potential security risks in Linux operating systems.

| Command |Description  |
| --- | --- |
| Whoami | Displays current username |
| id | Returns user identity  |
| hostname  | Sets or prints the name of current host system. |
| uname  | Prints basic information about the operating system name and system hardware. |
| pwd | Returns working directory name  |
| ifconfig  | The ifconfig utility is used to assign or to view an address to a network interface and/or configure network interface parameters. |
| ip | Ip is a utility to show or manipulate routing, network devices, interfaces and tunnels. |
| netstat | shows network status. |
| ss | Another utility to investigate sockets. |
| ps | Shows process status. |
| who | Displays who is logged in. |
| env | Prints environment or sets and executes command. |
| lsblk | Lists block devices. |
| lsusb | Lists USB devices |
| lsof | Lists opened files. |
| lspci | Lists PCI devices. |

## Logging In via SSH

Secure Shell (SSH) refers to a protocol that allows clients to access and execute commands or actions on remote computers. On Linux based hosts and servers, as well as other Unix-like operating systems, SSH is one of the permanently installed standard tools and is the preferred choice for many administrators to configure and maintain a computer through remote access. It is an older and very proven protocol that does not require or offer a graphical user interface (GUI). For this reason, it works very efficiently and occupies very few resources. We use this type of connection in the following sections, and in most of the other module lab exercises, to offer the possibility to try out the learned commands and actions in a safe environment.

We can connect to our targets with the following command:

![image.png](../images/snippets/System_Information/image.png)

Now, let us look at a few examples on the machine we have just logged in.

### Hostname

The hostname command is pretty self-explanatory and will just print the name of the computer that we are logged into

![image.png](../images/snippets/System_Information/image_1.png)

### whoami

This quick and easy command can be used on both Windows and Linux systems to get our current username. During a security assessment, we obtain reverse shell access on a host, and one of the first bits of situational awareness we should do is figuring out what user we are running as. From there, we can figure out if the user has any special privileges/access.

![image.png](../images/snippets/System_Information/image_2.png)

### Id

The id command expands on the whoami command and prints out our effective group membership and IDs. This can be of interest to penetration testers looking to see what access a user may have and sysadmins looking to audit account permissions and group membership. In this output, the hackthebox group is of interest because it is non-standard, the adm group means that the user can read log files in /var/log and could potentially gain access to sensitive information, membership in the sudo group is of particular interest as this means our user can run some or all commands as the all-powerful root user. Sudo rights could help us escalate privileges or could be a sign to a sysadmin that they may need to audit permissions and group
memberships to remove any access that is not required for a given user to carry out their day-to-day tasks.

![image.png](../images/snippets/System_Information/image_3.png)
### Uname

Let's dig into the uname command a bit more. If we type man uname in our terminal, we will bring up the man page for the command, which will show the possible options we can run with the command and the results.

![image.png](../images/snippets/System_Information/image_4.png)

Running uname -a will print all information about the machine in a specific order: kernel name, hostname, the kernel release, kernel version, machine hardware name, and operating system. The -a flag will omit -p (processor type) and -i (hardware
platform) if they are unknown.

![image.png](../images/snippets/System_Information/image_5.png)

From the above command, we can see that the kernel name is Linux, the hostname is box, the kernel release is 4.15.0-99-generic, the kernel version is #100-Ubuntu SMP Wed Apr 22 20:32:56 UTC 2020, and so on. Running any of these options on their own will give
us the specific bit output we are interested in.

### Uname to Obtain Kernal Release

Suppose we want to print out the kernel release to search for potential kernel exploits quickly. We can type uname -r to obtain this information.

![image.png](../images/snippets/System_Information/image_6.png)
With this info, we could go and search for "4.15.0-99-generic exploit," and the first [result](https://www.exploit-db.com/exploits/47163) immediately appears useful to us.

It is highly recommended to study the commands and understand what they are for and what information they can provide. Though a bit tedious, we can learn much from studying the manpages for common commands. We may even find out things that we did not even know were possible with a given command. This information is not only used for working with Linux. However, it will also be used later to discover vulnerabilities and misconfigurations on the Linux system that may contribute to privilege escalation. Here are a few optional exercises that we can solve for practice purposes, which will help us become familiar with some of the commands.