# 1.0 Simplified Docker Architecture

Docker or correctly, Docker Engine \(Docker runtime\) is:

* Docker Server: The Docker Daemon \(`dockerd`\) exposing a REST API. This daemon can co-ordinate with other daemons to manage images, containers, networks and volumes.
* Docker Client: A CLI which takes `docker` commands and talks to the Docker server

Additionally, you need

* Docker Registry: Storage for docker images. You can use a managed registry like [https://hub.docker.com/](https://hub.docker.com/) or host a private registry. Docker Daemon first searches for the image in it's local cache and then attempts to reach whatever registry is configured to host the Images.
* ![](https://docs.docker.com/engine/article-img/engine-components-flow.png)

Image: [https://docs.docker.com/engine/docker-overview/\#docker-engine](https://docs.docker.com/engine/docker-overview/#docker-engine)

Following image shows typical interaction when you execute a docker command![](https://docs.docker.com/engine/article-img/architecture.svg)Image: [https://docs.docker.com/engine/docker-overview/\#docker-architecture](https://docs.docker.com/engine/docker-overview/#docker-architecture)

# Exercise 1

1. What are the docker commands available?
2. Find the docker version.



