### Dir

Flag 	Long Flag 	Description
-c 	--cookies 	This flag configures a cookie to pass along each request, such as a session ID.
-x 	--extensions 	This flag specifies which file extensions you want to scan for. E.g., .php, .js
-H 	--headers 	This flag configures an entire header to pass along with each request.
-k 	--no-tls-validation 	This flag  skips the process that checks the certificate when https is used. It often happens for CTF events or test rooms like the ones on THM a self-signed certificate is used. This causes an error during the TLS check.
-n 	--no-status 	You can set this flag when you don’t want to see status codes of each response received. This helps keep the output on the screen clear.
-P 	password 	You can set this flag together with the --username flag to execute authenticated requests. This is handy when you have obtained credentials from a user.
-s 	--status-codes 	With this flag, you can configure which status codes of the received responses you want to display, such as 200, or a range like 300-400.
-b 	--status-codes-blacklist 	This flag allows you to configure which status codes of the received responses you don’t want to display. Configuring this flag overrides the -s flag.
-U 	--username 	You can set this flag together with the --password flag to execute authenticated requests. This is handy when you have obtained credentials from a user.
-r	--followredirect	This flags configures Gobuster to follow the redirect that it received as a response to the sent request. A HTTP redirect status code (e.g., 301 or 302) is used to redirect the client to a different URL.

#### Heading 4
