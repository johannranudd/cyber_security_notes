

[[meterpreter]]  (app://obsidian.md/meterpreter)  
[https://www.offsec.com/metasploit-unleashed/meterpreter-basics/](https://www.offsec.com/metasploit-unleashed/meterpreter-basics/)



#### shells
- ``use post/multi/manage/shell_to_meterpreter`` to convert to materpreter
- CTRL+Z to background shell
- inside meterpreter you can run `shell` to open a new shell and CTRL+Z too background.
- then find it again by running `channel -i {ID}`

- to get process ID: `getpid`
- if using `ps` command, the meterpreter will list as: spoolsv.exe and not Meterpreter.exe
- to find DLLs (Dynamic-Link Libraries) we can use tasklist /m /fi "pid eq 1304" if the PID is 1304

Meterpreter will provide you with three primary categories of tools;

```
Built-in commands
Meterpreter tools
Meterpreter scripting
```

If you run the help command, you will see Meterpreter commands are listed under different categories.

```
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
```

Please note that the list above was taken from the output of the help command on the Windows version of Meterpreter (windows/x64/meterpreter/reverse_tcp). These will be different for other Meterpreter versions.

Meterpreter commands

Core commands will be helpful to navigate and interact with the target system. Below are some of the most commonly used. Remember to check all available commands running the help command once a Meterpreter session has started.

Core commands

```
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
```

File system commands

```
cd: Will change directory
ls: Will list files in the current directory (dir will also work)
pwd: Prints the current working directory
edit: will allow you to edit a file
cat: Will show the contents of a file to the screen
rm: Will delete the specified file
search: Will search for files
upload: Will upload a file or directory
download: Will download a file or directory
```

Networking commands

```
arp: Displays the host ARP (Address Resolution Protocol) cache
ifconfig: Displays network interfaces available on the target system
netstat: Displays the network connections
portfwd: Forwards a local port to a remote service
route: Allows you to view and modify the routing table
```

System commands

```
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
```

Others Commands (these will be listed under different menu categories in the help menu)

```
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
```

#### migrate meterpreter

Migrating to another process will help Meterpreter interact with it. For example, if you see a word processor running on the target (e.g. word.exe, notepad.exe, etc.), you can migrate to it and start capturing keystrokes sent by the user to this process. Some Meterpreter versions will offer you the keyscan_start, keyscan_stop, and keyscan_dump command options to make Meterpreter act like a keylogger. Migrating to another process may also help you to have a more stable Meterpreter session.

To migrate to any process, you need to type the migrate command followed by the PID of the desired target process. The example below shows Meterpreter migrating to process ID 716.

- migrate 716

Be careful; you may lose your user privileges if you migrate from a higher privileged (e.g. SYSTEM) user to a process started by a lower privileged user (e.g. webserver). You may not be able to gain them back.

Commands mentioned previously, such as getsystem and hashdump will provide important leverage and information for privilege escalation and lateral movement.  
Finally, you can also use the `load` command to leverage additional tools such as Kiwi or even the whole Python language.

- meterpreter > `load python`

get current use: `getuid`  
get system privelege: `getsystem`