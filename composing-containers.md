# 4.0 Breaking down and building up

Most of you would break down monolithic applications into smaller services. A typical web application would consist of multiple front ends, API backends, data stores, proxy, caches, gateways, etc and you would be aware that each one of these 'services' would actually have different release schedules, contracts to satisfy, dependencies, run time requirements, different availabilities, thus clearly indicating that even though you may have built them separately, running them together in one container would be a bad idea. However, lets take a simple application, build a single Docker Image which runs the entire stack in it and start checking out reasons why we would want to break it down, and then finally once broken down, learn if there are tools to help us manage the atomic parts of the application.

# 4.1 Role of ENTRYPOINT

From [Docker best practices page](https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/#entrypoint)

> The best use for `ENTRYPOINT` is to set the image’s main command, allowing that image to be run as though it was that command \(and then use `CMD` as the default flags\).

An `ENTRYPOINT` can also be used to execute a shell script, which could do a multitude of things needed before a service started. For instance, it could be used to initialize databases, check start dependencies, just about anything necessary. Extending that use case, one may use the `ENTRYPOINT` to launch multiple processes for that monolithic container!

# 4.2 The monolithic container

Let's create a Dockerfile which runs a proxy, 1 front end served by 2 API back end services.

# Exercise 4.2

1. Create a single docker image which has both the sample app and nginx installed.
2. Copy a nginx configuration so that you can proxy the nodeJS app
3. Write a helper script to start both the nginx and nodeJS processes and add that to `ENTRYPOINT`
4. Run the docker image and go to `localhost` on your browser to see the hello world line. So, now you have 2 programs running in the same container.



