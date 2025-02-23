# Overview: Lab 6 Common Active Directory Issues, CMD Commands, PC Offline

This section of my home lab documentation explores common Active Directory issues, troubleshooting with CMD commands, and resolving situations where a PC is offline in a domain environment. The project provides practical solutions for addressing common problems that administrators face when working with Active Directory, such as authentication failures, group policy application issues, and troubleshooting offline PCs.

## Objectives

Identify and resolve common Active Directory issues, such as login problems and account lockouts.
Use CMD commands to troubleshoot and resolve issues related to domain connectivity, account authentication, and more.
Handle scenarios where a PC is offline from the domain, including troubleshooting network connectivity and domain membership.
Understand how to diagnose and repair issues using Active Directory logs, CMD commands, and network tools.

## Documentation

In this home lab, we will explore common Active Directory issues users might encounter, then use CMD commands to resolve PC offline problems.

Let's begin with some CMD commands. On the local user account Bob, open Command Prompt and type ping 12.1.10.2. This is the IP address of our Windows Server 2022 machine. This command will confirm that Desktop2 can communicate with the server. Now, let's repeat the process on the Server by pinging Desktop2 to verify the connection from the server side.
