---
title: Examining Group Policy Active Directory
slug: Examining_Group_Policy(AD)
description: Manageing the different users in Linux system   
image: ../images/snippets/Examining_Group_Policy.png
---

Group Policy is a Windows feature that provides administrators with a wide array of advanced settings that can apply to both user and computer accounts in a Windows environment. Every Windows host has a Local Group Policy editor to manage local settings. For our purposes, we will focus on Group Policy in a domain context for managing users and computers in Active Directory. Group Policy is a powerful tool for managing and configuring user settings, operating systems, and applications. Group Policy is also a potent tool for managing security in a domain environment. From a security context, leveraging Group Policy is one of the best ways to widely affect your enterprise's security posture. Active Directory is by no means secure "out of the box," and Group Policy, when used properly, is a crucial part of a defense-in-depth strategy. 

While Group Policy is an excellent tool for managing the security of a domain, it can also be abused by attackers. Gaining rights over a Group Policy Object could lead to lateral movement, privilege escalation, and even full domain compromise if the attacker can leverage them in a way to take over a high-value user or computer. They can also be used as a way for an attacker to maintain persistence within a network. Understanding how Group Policy works will give us a leg up against attackers and can help us greatly on penetration tests, sometimes finding nuanced misconfigurations that other penetration testers may miss.

### Group Policy Objects (GPOs)

A Group Policy Object (GPO) is a virtual collection of policy settings that can be applied to user(s) or computer(s). GPOs include policies such as screen lock timeout, disabling USB ports, enforcing a custom domain password policy, installing software, managing applications, customizing remote access settings, and much more. Every GPO has a unique name and is assigned a unique identifier (a GUID). They can be linked to a specific OU, domain, or site. A single GPO can be linked to multiple containers, and any container can have multiple GPOs applied to it. They can be applied to individual users, hosts, or groups by being applied directly to an OU. Every GPO contains one or more Group Policy settings that may apply at the local machine level or within the Active Directory context.

### Example GPOs

- Establishing different password policies for service accounts, admin accounts, and standard user accounts using separate GPOs
- Preventing the use of removable media devices (such as USB devices)
- Enforcing a screensaver with a password
- Restricting access to applications that a standard user may not need, such as cmd.exe and PowerShell
- Enforcing audit and logging policies
- Blocking users from running certain types of programs and scripts
- Deploying software across a domain
- Blocking users from installing unapproved software
- Displaying a logon banner whenever a user logs into a system
- Disallowing LM hash usage in the domain
- Running scripts when computers start/shutdown or when a user logs in/out of their machine

Let's use as example a default Windows Server 2008 Active Directory implementation, password complexity is enforced by default. The password complexity requirements are as follows:

- Passwords must be at least 7 characters long.
- Passwords must contain characters from at least three of the following four categories:
    - Uppercase characters (A-Z)
    - Lowercase characters (a-z)
    - Numbers (0-9)
    - Special characters (e.g. !@#$%^&*()_+|~-=`{}[]:";'<>?,./)

These are just a few examples of what can be done with Group Policy. There are hundreds of settings that can be applied within a GPO, which can get extremely granular. For example, below are some options that we can set for Remote Desktop sessions.

**Order of Precedence**

- Local Group - Policy The policies are defined directly to the host locally outside the domain. Any setting here will be overwritten if a similar setting is defined at a higher level.
- Site Policy - Any policies specific to the Enterprise Site that the host resides in. Remember that enterprise environments can span large campuses and even across countries. So it stands to reason that a site might have its own policies to follow that could differentiate it from the rest of the organization. Access Control policies are a great example of this. Say a specific building or site performs secret or restricted research and requires a higher level of authorization for access to resources. You could specify those settings at the site level and ensure they are linked so as not to be overwritten by domain policy. This is also a great way to perform actions like printer and share mapping for users in specific sites.
- Domain-wide Policy - Any settings you wish to have applied across the domain as a whole. For example, setting the password policy complexity level, configuring a Desktop background for all users, and setting a Notice of Use and Consent to Monitor banner at the login screen.
- Organizational Unit (OU) - These settings would affect users and computers who belong to specific OUs. You would want to place any unique settings here that are role-specific. For example, the mapping of a particular share drive that can only be accessed by HR, access to specific resources like printers, or the ability for IT
admins to utilize PowerShell and command-prompt.
- Any OU Policies nested within other OU's - Settings at this level would reflect special permissions for objects within nested OUs. For example, providing Security Analysts a specific set of
Applocker policy settings that differ from the standard IT Applocker settings.

We can manage Group Policy from the Group Policy Management Console (found under Administrative Tools in the Start Menu on a domain controller), custom applications, or using the PowerShell GroupPolicy module via command line. The Default Domain Policy is the default GPO that is automatically created and linked to the domain. It has the highest precedence of all GPOs and is applied by default to all users and computers. Generally, it is best practice to use this default GPO to manage default settings that will apply domain-wide. The Default Domain Controllers policy is also created automatically with a domain and sets baseline security and auditing settings for all domain controllers in a given domain. It can be customized as needed, like any GPO.

### GPO Order of Precedence

GPOs are processed from the top down when viewing them from a domain organizational standpoint. A GPO linked to an OU at the highest level in an Active Directory network (at the domain level, for example) would be processed first, followed by those linked to a child OU, etc. This means that a GPO linked directly to an OU containing user or computer objects is processed last. In other words, a GPO attached to a specific OU would have precedence over a GPO attached at the domain level because it will be processed last and could run the risk of overriding settings in a GPO higher up in the domain hierarchy. One more thing to keep track of with precedence is that a setting configured in Computer policy will always have a higher priority of the same setting applied to a user. The following graphic illustrates precedence and how it is applied.