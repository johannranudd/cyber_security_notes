 exploits used:

	- **SUCCESS** windows/smb/ms17_010_eternalblue 
		
		payload:
			- windows/x64/meterpreter/reverse_tcp
			- windows/x64/shell/reverse_tcp
		post: 
			- post/multi/manage/shell_to_meterpreter
			  
			  
			  
			  
			  
### nmap results

**445/tcp   open  microsoft-ds  Microsoft Windows 7 - 10 microsoft-ds (workgroup: WORKGROUP)**
