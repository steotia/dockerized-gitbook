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

Node App

1. Create an executable container which has node and npm installed with` npm install` as the default command
2. Use this container to install node modules \(in your local filesystem\) as mentioned in [https://github.com/steotia/nodejs-pipeline/blob/gitbook/src/package.json](https://github.com/steotia/nodejs-pipeline/blob/gitbook/src/package.json)
3. Add a layer to run `gulp bundle` and 

1. Take the source code at [https://github.com/steotia/nodejs-pipeline/tree/gitbook/src](https://github.com/steotia/nodejs-pipeline/tree/gitbook/src) 
2. Start with an base image of your choice
3. Copy the package.json and perform an `npm install`
4. Copy the source code and run the application
5. 


