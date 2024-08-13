```
openssl genpkey -algorithm RSA -out api_whatsapp.key -aes256
openssl req -new -key api_whatsapp.key -out api_whatsapp.csr\
openssl x509 -req -days 365 -in api_whatsapp.csr -signkey api_whatsapp.key -out api_whatsapp.crt
cat api_whatsapp.key api_whatsapp.crt > /etc/stunnel/api_whatsapp.pem

```
```
pid = /var/run/stunnel.pid

cert = /etc/stunnel/api_whatsapp.pem

[whatsapp]
accept = 8444
connect = 127.0.0.1:22
#sni = api.whatsapp.com
```
```
ssh -C -o "ProxyCommand=nc -X CONNECT -x 127.0.0.1:9092 %h %p" root@SERVER -p 8444 -CND 1080 -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null

```
```
Enjoy!
```
