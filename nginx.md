#### Basic Example of load balancing nginx.conf file

```
http {
    upstream backend {
        server 127.0.0.1:3000;
	    server 127.0.0.1:6100;
	    server 127.0.0.1:4000;
    }

    server {
        listen 80;
	    #this is comment
        location / {
            proxy_pass http://backend;
        }
    }
}

events {}
```

#### Run backend and fronend at same domain

```
location / {
    proxy_pass http://127.0.0.1:3000;
}
location /api {
	rewrite ^\/api\/(.*)$ /api/$1 break;
	proxy_pass http://localhost:3030;
}
```
