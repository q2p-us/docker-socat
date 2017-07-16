# docker-socat
### The simplest container with preinstalled socat

It is may be not so elegant but really easy way to connect isolated networks over unix socket.
For example to connect container from swarm's stack with container inside the Drone.io build system.

### Example

On the nginx (just for example) side:

`docker run --network nginx -d -v /var/run/socat_nginx:/var/run/socat_nginx --name socat_proxy q2pus/socat "UNIX-LISTEN:/var/run/socat_nginx/socat.sock,reuseaddr,fork" "TCP:nginx:80"`

On the isolated side:

`docker run --network isolated -d -v /var/run/socat_nginx:/var/run/socat_nginx:ro --name socat_nginx socat "TCP-LISTEN:80,fork" "UNIX-CONNECT:/var/run/socat_nginx/socat.sock"`
