```

openssl genpkey -algorithm RSA -out api.whatsapp.com.key -aes256 -pass pass:parolaniz

openssl req -new -key api.whatsapp.com.key -out api.whatsapp.com.csr -passin pass:parolaniz -subj "/C=TR/ST=YourState/L=YourCity/O=YourOrganization/OU=YourUnit/CN=api.whatsapp.com"

openssl x509 -req -days 365 -in api.whatsapp.com.csr -signkey api.whatsapp.com.key -out api.whatsapp.com.crt -passin pass:parolaniz

cat api.whatsapp.com.crt api.whatsapp.com.key > api.whatsapp.com.pem

```
```
pid = /var/run/stunnel.pid
output = /var/log/stunnel.log
cert = /root/api.whatsapp.com.crt
key = /root/api.whatsapp.com.key
#cert = /root/api.whatsapp.com.pem
#key = /root/api.whatsapp.com.pem

# TLS/SSL sunucusu
[ssh]
accept = 443
connect = 127.0.0.1:22

# Opsiyonel: TLS versiyonlarını belirtme (en güvenli versiyonları tercih edin)
#sslVersion = TLSv1.2
#options = NO_SSLv2
#options = NO_SSLv3
#options = NO_TLSv1
#options = NO_TLSv1.1

```

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
