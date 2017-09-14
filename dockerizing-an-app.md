# 3.0 Common Dockerfile commands

[https://docs.docker.com/engine/reference/builder/](https://docs.docker.com/engine/reference/builder/) describes the commands one can use in a Dockerfile. Typically, the commands commonly used are:

* **FROM**: Initialises build and sets the base image. Generally considered a good idea to take official, LTS images based on Alpine Linux. Also, important to lock down and specify the version in the image tag.
* **RUN**: Runs a shell command in a new layer
* **CMD**: Provides defaults \(executable or params to executable\) for a container. A `CMD` overrides any preceding `CMD` layers. Executable can be omitted if there is an `ENTRYPOINT`. `CMD` is different from `RUN`, since `RUN` actually runs and creates a layer whereas `CMD` gets run during container run
* **EXPOSE**: Tells Docker that a container is listening on that port. It does not open the port between the host and the container. For that use the `-p` or `-P` option in `docker run`.
* **ENV**: sets environment key value pairs. These values can be changed during `docker run`.
* **ADD**: Copies new files, directories and remote file URLs from source to destination. Note that the directory is not copied but the contents.
* **COPY**: Is simpler than `ADD`.
* **ENTRYPOINT**: Configures a container to run as an executable. 
* **VOLUME**: Creates a mount point to share files from the host system. However, the filesystem from the host machine needs to be mounted at this point when doing a `docker run`.
* **USER: **Changes the user \(and group\) for subsequent instructions.
* **WORKDIR**: Sets the working directory. Once set, subsequent commands can take relative paths.
* **ARG**: Used to pass in variables during build time

# Exercise 3.0.1

Start from a Base image of your choice and do the following

**Exercise 3.0.1.1** build a NPM executable

1. Create an Image which can run `npm install`. Create a `package.json` and copy it inside the image. Run this image and note if the dependencies are installed every time. Why?
2. Change the Image to install the dependencies in the Image itself.
3. Share the node\_modules folder when running the container so that npm runs inside the container but the dependencies get installed outside.

**Exercise 3.0.1.2** Dockerize a Node app

1. Take the source at [https://github.com/steotia/sample-nodejs](https://github.com/steotia/sample-nodejs) and dockerize it to run on port 3000.

_Hint: You will need to take a base image with node, copy the source code, do an npm install, expose port 3000 and finally run it_



