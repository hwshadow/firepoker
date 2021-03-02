```
openssl req -x509 -new -nodes -keyout domain.key -out domain.crt -days 365
htpasswd -c ngnix.htpasswd user
```