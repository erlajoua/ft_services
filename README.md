## ft_services

### Description ✨
Creation of a Kubernetes cluster with several containers communicating with each other, containing the following services
- Web Server Nginx
- Wordpress
- PhpMyAdmin
- Grafana
- FTPS
- DB InfluxDB
- MySQL DB

The cluster works with Minikube, each service must have a dedicated container.
All containers are built on Alpine Linux.
Each container has been created by a custom Dockerfile.

Each container must be able to restart automatically in case of a crash.
The main service of each container must be able to restart automatically in case of a crash.
The data of the database containers must persist in case of a crash.

### Main purpose :page_facing_up:

The cluster works with Minikube. 
All containers are built on Alpine Linux via a hand-created Dockerfile.

Creation of a kubernetes cluster (minikube)
Installation of a Load Balancer, MetalLB which will be the entry point of the cluster to all other services.
- A container for Wordpress on port 5050, working with the MySQL DB container, this container has its own nginx web server.
- A container for PhpMyAdmin on port 5000, also connected to the MySQL DB.
- A container for the Nginx web server on port 80 and 443 for SSL. The server is in HTTP on port 80 and then is redirected with a 301 redirect in HTTPS on port 443. A redirect with /wordpress makes a 307 redirect to the Wordpress, and also an access to PhpMyAdmin in reverse proxy.
- A container for FTPS on port 21.
- A Grafana container on port 3000, which via the InfluxDB DB manages the monitoring of all other containers.

_Each container has a liveness probe set up to restart the main service inside each container._

### How to use :rocket:

Run
```
./setup.sh
```
