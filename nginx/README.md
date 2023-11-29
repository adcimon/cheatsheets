# NGINX

<p align="center"><img align="center" width="50%" height="50%" src="assets/nginx.svg"></p>

[NGINX](https://www.nginx.com/) is a web server that can also be used as a reverse proxy, load balancer, mail proxy and HTTP cache.

Upgrade to WebSocket.
```
proxy_set_header  Upgrade $http_upgrade;
proxy_set_header  Connection "Upgrade";
```

Keep real client IP address.
```
proxy_set_header  X-Real-IP $remote_addr;
proxy_set_header  X-Forwarded-For $proxy_add_x_forwarded_for;
proxy_set_header  X-Forwarded-Host $server_name;
```

Redirect requests removing the API version.
```
server {
  ...
  location ~ ^/v1(/.*) {
    ...
    rewrite ^/v1(/.*)$ $1 break;
    ...
  }
}
```
