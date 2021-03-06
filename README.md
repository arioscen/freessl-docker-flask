# freessl-docker-flask 

### 1.申請 Domain
### 2.在 ubuntu主機 安裝 Certbot，自動更新 SSL 憑證
[How To Secure Apache with Let's Encrypt on Ubuntu 16.04](https://www.digitalocean.com/community/tutorials/how-to-secure-apache-with-let-s-encrypt-on-ubuntu-16-04)
### 3.編輯 Dockerfile
預設用動態輸入方式指定 DOMIAN
```
CMD gunicorn -w 3 -b 0.0.0.0:5000 wsgi \
--keyfile /etc/letsencrypt/live/$DOMAIN/privkey.pem \
--certfile /etc/letsencrypt/live/$DOMAIN/cert.pem \
--ca-certs /etc/letsencrypt/live/$DOMAIN/fullchain.pem
```
### 4.建立 Docker Image
```
sudo docker build -t <yourImageName> <DockerfileFolder>
```
### 5.執行 Container
```
sudo docker run -it -d -p 5000:5000 -v /etc/letsencrypt:/etc/letsencrypt \
-e DOMAIN=<yourDomain> <yourImageName>
```
### 6.連線web
```
https://<yourDomain>:5000
```