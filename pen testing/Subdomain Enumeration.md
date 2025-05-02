
## OSINT - SSL/TLS Certificates
- search databse for SSL/TSL certificates: https://crt.sh/ 


## OSINT - Search Engines

## DNS Bruteforce

`user@thm:~$ dnsrecon -t brt -d acmeitsupport.thm`

## OSINT - Sublist3r

`user@thm:~$ ./sublist3r.py -d acmeitsupport.thm`

## Virtual Hosts

           
user@machine$ ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt -H "Host: FUZZ.acmeitsupport.thm" -u http://10.10.180.222

        
                   
user@machine$ ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt -H "Host: FUZZ.acmeitsupport.thm" -u http://10.10.180.222 -fs {size}