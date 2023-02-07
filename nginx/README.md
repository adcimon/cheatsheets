# NGINX

<p align="center"><img align="center" width="50%" height="50%" src="assets/nginx.svg"></p>

[NGINX](https://www.nginx.com/) is a web server that can also be used as a reverse proxy, load balancer, mail proxy and HTTP cache.

Keep real client IP address.
```
proxy_set_header  X-Real-IP $remote_addr;
proxy_set_header  X-Forwarded-For $proxy_add_x_forwarded_for;
```
