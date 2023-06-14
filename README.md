# docker-apprtc

#### Table of Contents
* [Prepare](#Prepare)
* [Get Template Project](#get-template-project)
* [Change Config](#change-onfig)
* [Start](#start)

----

## Prepare
1. Install docker
2. Install docker-compose
3. domain
4. certs for domain

----

## Get Template Project
* clone the docker-apprtc project

```
git clone git@github.com:yunqiic/docker-apprtc.git
```

----

## Change Config

### .env
* change PUBLIC_IP to your public ip

- PUBLIC_IP

### constants.py in config dir
* Change the url domain
* This project will use https and wss

- ICE_SERVER_BASE_URL
- WSS_INSTANCE_HOST_KEY

### nginx.conf in nginx-conf dir
* change the server_name to your domain
* You can the ssl_certificate config if you like, but you should make sure that you have the file. You can check the file path in docker-compose.yml

- server_name
- ssl_certificate
- ssl_certificate_key

### docker-compose.yml
* change the volumns config `/cert/yourdomain.com:/cert`. The path `/cert/yourdomain.com` and certs file should exist in your host machine, and the certs file'name should be as the same as ssl_certificate, ssl_certificate_key config in the nginx.conf

- volumes in apprtc-web

----

## Start

```
sudo docker-compose up -d
```

----

## Enjoy
* enjoy it by your url, like https://yourdomain.com. The url should be configured in the nginx.conf.