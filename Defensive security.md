
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