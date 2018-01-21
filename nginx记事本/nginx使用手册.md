# nginx 使用手册
## 常用命令

 1. windows环境下

至nginx.exe目录，cmd中执行start nginx

|功能| 命令 |
|---------|-------|
|启动| start nginx |
|  重启       | nginx -s reload |
|关闭|nginx -s stop或者nginx -s quit|

## nginx负载均衡

一个简单的负载均衡，把ghlp.lidechenyan.club均衡到本机不同的端口

    http {
		upstream ghlp {
			server 127.0.0.1:8013 weight=3;
			server 127.0.0.1:8014;
		}
		server {
	        listen       80;
	        server_name  ghlp.lidechenyan.club;
	        location / {
	            root   html;
	            index  index.html index.htm;
				proxy_pass http://ghlp;
	        }
		}
	}


## nginx反向代理

实现方式，编辑nginx.conf，配置upstream和location

    server {
        listen       443 ssl;#监听443端口，并启动ssl
        server_name  ghlp.lidechenyan.club;#域名设置
        ssl_certificate      cert.pem;
        ssl_certificate_key  cert.key;
        ssl_session_cache    shared:SSL:1m;
        ssl_session_timeout  5m;
        ssl_ciphers  HIGH:!aNULL:!MD5;
        ssl_prefer_server_ciphers  on;
        location / {
            root   html;
            index  index.html index.htm;
			proxy_pass http://ghlp;#反向代理，ghlp在upstream中设置
        }
    }
