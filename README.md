# docker-apprtc

#### Table of Contents
* [Prepare](#Prepare)
* [Get Template Project](#get-template-project)
* [Change Config](#change-config)
* [Start](#start)
* [Enjoy](#enjoy)
* [Donate](#donate)

----

## Prepare
1. Install docker
2. Install docker-compose
3. domain
4. certs for domain
5. make sure that there is no nginx running

----

## Get Template Project
* clone the docker-apprtc project

```
git clone https://github.com/yunqiic/docker-apprtc.git
```

----

## Change Config

### .env
* change PUBLIC_IP to your public ip

```
PUBLIC_IP=127.0.0.1
```

### constants.py in config dir
* Change the url domain
* This project will use https and wss

```python
ICE_SERVER_BASE_URL = 'https://yourdoamin.com'
WSS_INSTANCE_HOST_KEY: 'yourdoamin.com'
```

### nginx.conf in nginx-conf dir
* change the server_name to your domain
* You can update the ssl_certificate config if you like, but you should make sure that you have the file. You can check the file path in docker-compose.yml
* The path in nginx.conf should be the container path, not the host path.

```
ssl_certificate /cert/fullchain.pem;
ssl_certificate_key /cert/privkey.pem;

server_name yourdomain.com www.yourdomain.com;
```

* The `randomcalling` is the url path you want to visit, like https://yourdomain.dom/randomcalling
* There are two `randomcalling` you need to update.

```
# https://yourdomain.dom/randomcalling
location /randomcalling {
    # 转向代理的地址
    proxy_pass http://roomserver;
    proxy_redirect    off;
    proxy_set_header Host $host;
    rewrite ^/randomcalling(.*) /$1 break;
}

# https://yourdomain.dom/randomcalling1
location /randomcalling1 {
    # 转向代理的地址
    proxy_pass http://roomserver;
    proxy_redirect    off;
    proxy_set_header Host $host;
    rewrite ^/randomcalling1(.*) /$1 break;
}
```

### docker-compose.yml
* change the volumns config `/cert/yourdomain.com:/cert`. The path `/cert/yourdomain.com` and certs file should exist in your host machine, and the certs file'name should be as the same as ssl_certificate, ssl_certificate_key config in the nginx.conf
* `/cert/yourdomain.com` is the host path

```yaml
volumes:
    - /cert/yourdomain.com:/cert # see ssl_certificate, ssl_certificate_key config in nginx.conf under nginx-conf dir. make sure you have the file
```

#### example
* If you change the `/cert` behind `:`, you need to change the nginx.conf too.
* make sure the host path `/etc/letsencrypt/yourdomain.com` is not the symbolic links

```yaml
volumes:
    - /etc/letsencrypt/yourdomain.com:/cert # see ssl_certificate, ssl_certificate_key config in nginx.conf under nginx-conf dir. make sure you have the file
```

----

## Start

```
sudo docker-compose up -d

# check the service
sudo docker-compose ps

# check the log
sudo docker-compose logs -f
```

----

## Enjoy
* enjoy it by your url, like https://yourdomain.com. The url should be configured in the nginx.conf.

----

<table border="0">
	<tbody>
		<tr>
			<td align="center" valign="middle">
				<a href="https://url.cn/5jVTRwI" target="_blank">
					<!--<img height="120" src="https://wx4.sinaimg.cn/mw690/46b94231ly1ge0pvo2necj209l05kq3c.jpg">-->
					<img height="120" src="https://aigc.7otech.com/wp-content/uploads/2025/05/tencent.jpeg">
				</a>
			</td>
			<td align="right" valign="middle">
				<!--<img height="120" src="https://wx2.sinaimg.cn/mw690/46b94231ly1ge0po9ko70j20fk0fkjsc.jpg">-->
				<img height="120" src="https://aigc.7otech.com/wp-content/uploads/2025/05/fenxiang.jpeg">
			</td>
			<td align="center" valign="middle">
				<a href="https://www.vultr.com/?ref=8546025-6G" target="_blank">
					<!--<img height="120" src="https://wx3.sinaimg.cn/mw1024/46b94231ly1ge0p76k64bj206o06owev.jpg">-->
					<img height="120" src="https://aigc.7otech.com/wp-content/uploads/2025/05/vultr.jpeg">
				</a>
			</td>
			<td align="center" valign="middle">
				<a href="https://www.aliyun.com/minisite/goods?userCode=tewwu0c8" target="_blank">
					<!--<img height="120" src="https://img.alicdn.com/tfs/TB1Gc3zmAL0gK0jSZFxXXXWHVXa-259-194.jpg">-->
					<img height="120" src="https://aigc.7otech.com/wp-content/uploads/2025/05/aliyun.jpeg">
				</a>
			</td>
		</tr>
	</tbody>
</table>

## 捐助 donate

<table border="0">
	<tbody>
	    <tr>
	        <td>支付宝</td>
	        <td>微信</td>
	    </tr>
		<tr>
			<td align="left" valign="middle">
                <!--<img height="120" src="https://wx4.sinaimg.cn/mw690/46b94231ly1ge0okee0fej20ec0e6gp3.jpg">-->
                <img height="120" src="https://aigc.7otech.com/wp-content/uploads/2025/05/alipay.jpeg">
			</td>
			<td align="center" valign="middle">
				<!--<img height="120" src="https://wx4.sinaimg.cn/mw690/46b94231ly1ge0okecldyj20e80e8n0c.jpg">-->
				<img height="120" src="https://aigc.7otech.com/wp-content/uploads/2025/05/wechat.jpeg">
			</td>
		</tr>
	</tbody>
</table>

### Paypal
* [Paypal](https://paypal.me/zhangchunsheng)
