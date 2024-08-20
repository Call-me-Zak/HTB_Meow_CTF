# CTF Writeup for Meow on HTB platform

### Briefing:

This is a CTF writeup done in a sandbox provided by HTB platform. Both instances of the virtual machines are provided by HTB.

### Phase 0 : Accessing the sandbox on HTB

Spin up a VM instance (follow HTB instructions)

![image](https://github.com/user-attachments/assets/c1ff7f3a-887e-4cf5-8229-a8827b4339f2)

Open up cmd prompt

![image](https://github.com/user-attachments/assets/a3961aee-8856-47d7-8848-3b55af27e37f)

Check if the connection to the other machine is properly established by using ```ping <ip_address>```
0% packet loss = good.

![image](https://github.com/user-attachments/assets/7212fac2-c4e8-4d6a-8afa-a3babd267480)

### Phase 01 : Enumeration

In this phase we want to collect as many information on the other machine as possible. As the more we know the more we can increase the number of attack vectors along with the attack surface.

##### nmap

The tool we'll be using is ```nmap``` to scan for open ports : this tool will send requests to the other machine in hopes of getting a response, if there's a response then that port is open, to get a verbose output we'll be using the -V flag along with the -s service detection flag to determine the name and description of the service identified. And we'll be using sudo (SuperUserDO for elevated privileges)

```sudo nmap -sV <ip_address_of_the_other_machine>```

![image](https://github.com/user-attachments/assets/8ab3215c-45dc-4b5f-990e-2b302693a96c)

The scan has returned that port 23 is using "telnet" which is a protocol used for remote control of virtual terminals

![image](https://github.com/user-attachments/assets/4666efee-f4f0-4dd8-9846-4787b94259ea)

The host can receive telnet requests from other machines on the same network, and since the lab was set up so that we're already on the same network as the other virtual machine, we can go ahead and do just that.

The command is : ```telnet <ip_address_of_the_other_machine```, after running the command we're prompted to enter login credentials for the "Meow" account, which we don't have, and since there're no other ports available we can't really do much except go for an old fashioned brute force attack, but given the difficulty of the lab, before we commit to making a wordlist dictionary to initiate the attack, we can instead try common passwords & usernames manually : user/user - admin/admin - etc... and some use passwordless login (usually paired with SSO integration, but thankfully the difficulty of the lab begs to differ-- you can check one of my repos as I did a project on securing logins with SSO integration using Python)

Spent too much time so the request timed out, will have to resend another

![image](https://github.com/user-attachments/assets/3c3d517f-ffe3-40cf-b609-a2955161c46b)

After using different credentials, and getting to root/root, it worked out, matter of fact didn't even need a password.

![image](https://github.com/user-attachments/assets/be3aa378-1e00-4048-851f-6e2e9e4d2413)

Navigate the directories either using ```dir``` or ```ls``` to list all directories available

![image](https://github.com/user-attachments/assets/b04ac24a-eb28-490d-b16b-72dd237c25e3)

![image](https://github.com/user-attachments/assets/135376d2-3323-437f-92f2-231e09d8ec2a)

We found our ```flag.txt``` file, in order to read its contents we'll use the ```cat``` command to display all its contents.

And that's it !

![image](https://github.com/user-attachments/assets/06d7b90f-4c05-430f-8c88-93d66231387c)

![image](https://github.com/user-attachments/assets/94dccaa3-7dc9-4033-bf1f-4ad01d539fdf)

