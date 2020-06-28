# The Lifecycle of a Container

One thing that people generally worry about when using containerization in their tech stack is persistance.

Luckily, Docker containers have the capability to persist data after they have been stopped and started again. In fact, it is not until you run the docker remove command (docker rm) that a container's data gets deleted.

Let's look at a more complex command:

```
docker run -d --name web -p 80:8080 [namespace]/[image name]
```

We already know what "docker run" does.

The -d flag tells the deamon to start the container in detached mode. Meaning that it will run in the background and not attach to the current terminal. If we wanted to interact with the container we could instead use the -it flag and then append /bin/bash to the command to enter the container and interact with it.

The --name flag just allows us to name our container.

The -p flag tells the deamon which ports to map to. The image, which can be anything, is most likely a web service here since we are using port 8080. The 80:8080 argument tells the daemon to map port 80 on the docker host to 8080 on the container. This means that when we go to access the UI at a URL, we can use port 80.

Something different about how I specified the image name here, is that I prepended it with a namespace. An example being jamesmhare/image-name.

The reason you may sometimes have to do this is that you may be using what is called a second level image. We have already worked with first level images (these are images that live at the root level on Docker Hub and are maintained by official teams). However, second level images are stored in their own namespace and are generally less-offical images that a user maintains. That means that none of the second level images are really all that trustworthy. They may be less secure and you are really at the mercy of the developer.

So let's take a quick look at running a container and interacting with it. As mentioned above, we can use the -it flag instead of the -d flag to interact with the containers when using docker run:

```
docker run -it --name web -p 80:8080 [namespace]/[image name] /bin/bash
```

Remember to append /bin/bash to the end of the command. This tells the daemon to start the container with bash running.

You will notice that you command prompt has changed and that you are now inside your running container.

You can now run all the commands that you may be familiar with (ls, cd, top, etc.) and execute them in the container. One thing to remember is that you cannot just use the exit command to get out of the container as, since /bin/bash is probably the only process running in the container, if you exit out of your docker run command, you will kill the /bin/bash process and the container will automatically stop because it doesn't have any other processes running. Instead, you should use ctrl + p + q.


## Cleaning Up Containers

At this point, I wanted to introduce some other commands that can be useful in cleaning up running containers. This can be helpful when you have a lot of contianers running and you want to interact with them all.

To stop all containers, execute the following command:

```
docker stop $(docker ps -aq)
```

To remove all containers, execute the following command:

```
docker rm $(docker ps -aq)
```

To remove all images, execute the following command:

```
docker rmi $(docker ps -aq)
```

Running these three commands will ensure that you have Docker back to the original state as it was when we first started. It's a good way to wipe the slate clean and start over, if you need to.