# 4.0 Breaking down and building up

Most of you would break down monolithic applications into smaller services. A typical web application would consist of multiple front ends, API backends, data stores, proxy, caches, gateways, etc and you would be aware that each one of these 'services' would actually have different release schedules, contracts to satisfy, dependencies, run time requirements, different availabilities, thus clearly indicating that even though you may have built them separately, running them together in one container would be a bad idea. However, lets take a simple application, build a single Docker Image which runs the entire stack in it and start checking out reasons why we would want to break it down, and then finally once broken down, learn if there are tools to help us manage the atomic parts of the application.

# 4.1 Role of ENTRYPOINT

From [Docker best practices page](https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/#entrypoint)
> The best use for `ENTRYPOINT` is to set the image’s main command, allowing that image to be run as though it was that command \(and then use `CMD` as the default flags\).

An `ENTRYPOINT` can also be used to execute a shell script, which could do a multitude of things needed before a service started. For instance, it could be used to initialize databases, check start dependencies, just about anything necessary. Extending that use case, one may use the `ENTRYPOINT` to launch multiple processes for that monolithic container!

# 4.2 The monolithic container

Let's create a Dockerfile which runs a proxy, 1 front end served by 2 API back end services.

# Exercise 4.2

1. Start with the nginx image which you created in Ex 2.3.3.1
2. Add the lines from Ex. 3.1.1.2 to get a nodeJS front end
3. Write a helper script to start both the nginx and nodeJS processes and add that to `ENTRYPOINT`. You can expose different ports to access both nginx and nodeJS application.
4. Edit nginx configuration to setup a nginx upstream to the nodeJS application on `/frontend`. So, `localhost:3000/frontend` should show Hello World from your nodeJS application. Remove the application port from the Dockerfile.
5. Tag your image correctly and upload to your `hub.docker` registry




