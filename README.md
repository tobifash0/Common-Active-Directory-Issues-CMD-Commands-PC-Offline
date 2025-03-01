# Overview: Lab 6 Common Active Directory Issues, CMD Commands, PC Offline

This section of my home lab documentation explores common Active Directory issues, troubleshooting with CMD commands, and resolving situations where a PC is offline in a domain environment. The project provides practical solutions for addressing common problems that administrators face when working with Active Directory, such as authentication failures, group policy application issues, and troubleshooting offline PCs.

## Objectives

Identify and resolve common Active Directory issues, such as login problems and account lockouts.
Use CMD commands to troubleshoot and resolve issues related to domain connectivity, account authentication, and more.
Handle scenarios where a PC is offline from the domain, including troubleshooting network connectivity and domain membership.
Understand how to diagnose and repair issues using Active Directory logs, CMD commands, and network tools.

## Documentation

In this home lab, we will explore common Active Directory issues users might encounter, then use CMD commands to resolve PC offline problems.

Let's begin with some CMD commands. On the local user account Bob, open Command Prompt and type ping 192.168.1.100. This is the IP address of our Windows Server 2022 machine. This command will confirm that Desktop2 can communicate with the server. Now, let's repeat the process on the Server by pinging Desktop2 to verify the connection from the server side.
<br>

![Screenshot 2025-02-28 at 3 26 20 PM](https://github.com/user-attachments/assets/9fade4ad-f955-48ac-ae2c-e7d84b1f9aa9)

<br> 
1. Now on our Windows Server 2022, when we ping 192.168.1.102 (local user Bob), we can see that the connection timed out. This is because the firewall on that account is preventing the ping, so we would need to disable it. To do that, open up Windows Defender Firewall → Turn off Windows Defender Firewall on or off.

<br>

![Screenshot 2025-02-28 at 3 37 16 PM](https://github.com/user-attachments/assets/37108d4e-d791-4f2d-9748-32eeacba79db)

<br>

2. Use the Helpdesk administrative login to access Windows Defender Firewall, then turn off all of the options. Afterward, select OK to apply the changes.

<br>

![image](https://github.com/user-attachments/assets/0fb7edcf-e83d-4661-97c0-229636cde3ae)

<br> 

3. Now lets run the command line again on our Windows Server 2022.

<br>

![Screenshot 2025-02-28 at 3 26 20 PM](https://github.com/user-attachments/assets/25c46b4a-5ba0-455a-ab76-005bb049efc4)

<br>

4. If we add the -t option to our ping command, such as ping 192.168.1.100 -t, it will continue running indefinitely until manually stopped. This allows us to monitor network connectivity and observe any changes in packet loss over time. The ping will automatically stop if the Desktop2 PC is shut down or restarted.

<br.

![Screenshot 2025-02-28 at 3 37 48 PM](https://github.com/user-attachments/assets/eafa51ee-2299-4a61-9d75-6dc0fe7d49f3)

<br> 

5. Next, on the local user Bob, run Command Prompt as an administrator using the Helpdesk administrative login. Then, type gpresult /r > c:\results.txt. 

<br>

![image](https://github.com/user-attachments/assets/aa8c347a-ed57-4e50-beeb-0977b9176caa)

<br>

6. This command will generate a group policy report for the PC and save it as a text file in the C: drive.

<br>

![Screenshot 2025-02-28 at 3 44 42 PM](https://github.com/user-attachments/assets/f4ab0aa7-24ef-4d1f-8d42-1b110de33f4a)

<br>

7. If we do not run it in administrative then the command line will deny us access.

<br> 

![Screenshot 2025-02-28 at 3 41 46 PM](https://github.com/user-attachments/assets/2b196169-e6b5-4a80-81c5-f1806ea64929)

<br>

8. Some additional command lines such as gpupdate /help will provide a list of available options for the gpupdate command.

<br> 

![Screenshot 2025-02-28 at 3 49 14 PM](https://github.com/user-attachments/assets/ff61aeba-2cf6-4023-b6ab-c01e6f5e8dbc)

<br>

9. Gpresult /? will display a list of available options for the command.

<br> 

![image](https://github.com/user-attachments/assets/690f735b-4d6d-4c38-be67-6baddaa7f9cd)

<br> 

10. Gpresult /r displays the result of the Group Policy for the current user and computer.

<br> 

![Screenshot 2025-02-28 at 3 49 14 PM](https://github.com/user-attachments/assets/4af788b7-ea72-4964-9973-c130be8e53b2)

<br>

11. Next, let's explore some common issues that Helpdesk teams may encounter when assisting users, such as when a user account becomes locked out. To test this, we will sign out of Bob and purposely lock his account by putting the incorrect password.

<br>

![image](https://github.com/user-attachments/assets/b13e6824-0aa0-4be1-9152-13adbffe8d7d)

<br>
12. In this scenario when a user is locked out and is calling the helpdesk or admins for help, typically they would access the Active Directory Users and Computers → search for the user then unlock it from there. Lets try this out on our Helpdesk account. Open up Active Directory Users and Computers → right-click on the domain SimoTech.com and search up Bob, make sure that the entire directory is selected. Once Bob is found, double click on his name and select “Account” then select “Unlock Account”. then press “Apply” then “OK”. Now Bob can log into his account successfully.

<br>

![image](https://github.com/user-attachments/assets/3342ec27-a92a-4d52-96dc-17e8ff8c8079)

<br>

13. Bob should be able to log in now once his account is unlocked.

<br>

![Screenshot 2025-02-28 at 3 54 24 PM](https://github.com/user-attachments/assets/c1a3152f-e252-484d-a118-18a671325e78)

<br> 

14. Now let’s create an issue where Bob’s account is disabled for some reason and that he forgot his password. Let’s intentionally disable Bob’s account by clicking on his account again in Active Directory Users and Computers on the Helpdesk machine.

<br> 

![Screenshot 2025-02-28 at 3 57 58 PM](https://github.com/user-attachments/assets/6803b0e4-2e9f-4112-b8e5-e76a481c9ff1)

<br>

15. Now let’s imagine a scenario where Bob’s account is disabled for some reason, and he does not remember his password. 
<br> 

![image](https://github.com/user-attachments/assets/b323a51c-bb33-46f7-bcef-da06ab863276)

<br> 

16. As a helpdesk, we can look up Bob’s user in Active Directory Users and Computers using the Find command on the domain → select Entire Directory and search for Bob → right-click on his name and select Enable Account.


![Screenshot 2025-02-28 at 4 02 01 PM](https://github.com/user-attachments/assets/018676e5-635e-44e2-80d4-82569046272c)

<br>

17. Since Bob has forgotten his password, we can provide him with a temporary password that will allow him to log in and change it to his own password upon his next login. To do this, right-click on Bob and select Reset Password. Ensure that the User must change password at next logon option is enabled.

<br> 

![image](https://github.com/user-attachments/assets/51674d9c-cc64-4ad7-85d5-168bd9c39dcb)

<br> 

18. <br>  ![image](https://github.com/user-attachments/assets/a9ea3485-a1d9-4253-adf0-402950813c8c)

<br> 
19. 

