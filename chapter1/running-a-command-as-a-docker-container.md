# 1.1 Hello World

Lets take a simple long running command as `while true; do echo hello world; sleep 1; done` and try to run it in different environments to get a feel of basic docker commands.

## Exercise 1.1

1. Try it in a
   1. terminal
   2. Ubuntu container
   3. Alpine container
2. Check what Images got downloaded and their sizes
3. List containers
4. Remove all exited containers
5. Learn the usage of `--rm`
6. Run the Alpine container again in detached mode `-d`
7. Get access to container logs \(`STDOUT` and `STDERR`\)
8. Stop the container

_Hint_

`docker run --rm alpine sh -c "while true; do echo hello world; sleep 1; done"`

# 1.2 What is a Docker Image?

As shown earlier, when you do a `docker run` docker daemon pulls the image from a registry. Actually, `docker run` is a combination of `docker pull` and `docker start`. As the name suggests, pull pulls the image and start takes the image and runs the image as a Docker container.

When you do `docker pull ubuntu` the following \(or similar\) things happen:

![docker pull ubuntu](/assets/Screen Shot 2017-09-13 at 3.27.32 PM.png)

The Ubuntu image which gets downloaded is the same image for everyone \(provided that the tag is the same, preferably not `latest`\), and hence is portable across different environments and Host OS. This is possible because all docker installations run a Docker Engine on the Host OS \(and if the Host OS is not compatible, e.g. on Windows and Mac machines, a lightweight Unix VM is installed\) and all containers are spawned on the same Kernel of that VM with namespace isolations \(we will look at cgroups and namespaces later\).

Exercise 1.2

1. Run 2 containers and observe that these containers are in the process list of your Host OS \(Mac\)
2. Kill the process and observe the effect on the container

# 1.3 Docker Image fundamentals

Note that when you pulled in `ubuntu` there are 5 `Pull Complete` messages. Now lets understand at the construction of a Docker Image.

## Dockerfile

A Dockerfile is a text file which contains all instructions needed to create a Docker Image. Even Ubuntu or Alpine images we tried earlier have a Dockerfile and each line in a Dockerfile is a separate layer and has an ID \(digest\).

### Exercise 1.3.1

1. Find out the Dockerfiles representing the `ubuntu` and `alpine` images we pulled earlier and match the number of lines in the Dockerfiles to the number of `Pull Completes`. \(You need not try to understand what's happening at each layer of these Dockerfiles yet!\)

You will notice that each line in a Dockerfile matches to a separate Pull. These lines result in what are called as Layers. So, essentially, a Docker Image is created by taking a base image \(which in itself maybe a combination of N layers\) and incrementally changing it via as many layers as required. Note that all layers other than the last one are read only and hence can be re-used between different Images.

![](https://docs.docker.com/engine/userguide/storagedriver/images/container-layers.jpg)

Image: [https://docs.docker.com/engine/userguide/storagedriver/imagesandcontainers/\#images-and-layers](https://docs.docker.com/engine/userguide/storagedriver/imagesandcontainers/#images-and-layers)

`docker ps -s` gives a list of containers with the size of the container layer and the virtual size of the read only Image data.

It is important to know that an Image is broken down and built as layers because when an Image is edited, all layers from the changed layer to the end of the Dockerfile \(except the last layer, which is read write\) are re-built. So, layers which are least expected to change are pushed to the beginning of the Dockerfile and the layers which would change more often are pushed towards the end.

[https://docs.docker.com/engine/userguide/eng-image/dockerfile\_best-practices/](https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/) lists all the best practices and commands which are good to know when creating a Dockerfile. \(Read it at leisure\)

So, lets start create a few Dockerfiles:

###### Docker container with git installed

Dockerfile

```
FROM alpine:latest
RUN apk update
RUN apk add git
```

### Exercise 1.3.2



