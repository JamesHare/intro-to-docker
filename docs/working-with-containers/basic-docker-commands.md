# The Basic Docker Commands

One of the best things about Docker is that it works the exact same way across all platforms. The idea is that you build once and run anywhere.

The first command you should run after installing Docker is the version command:

```
docker version
```

In the output you will see the client and server versions running locally on the machine that you're logged onto.

The next command you should run is the docker info command:

```
docker info
```

The output will show how many containers and containers you have (how many are running, paused and stopped), how many images you have, the total number CPUs Docker is using, etc.

The next command you should run is the Docker Run command:

```
docker run hello-world
```

Let's break this down a bit further.

1. All Docker commands will start with "docker" which calls the Docker binary in the background.
2. "run" is the standard way of asking Docker to run a new container.
3. "hello-world" is the image that you want Docker to run.

After hitting return, the client goes and talks to the deamon. The Daemon will check to see if it has a copy of the hello-world image stored locally. If this is the first time you are running this command, it won't be stored locally yet. So the daemon will go and pull the image from Docker Hub, which I will write about later in this guide. The deamon takes the image from Docker Hub and uses it as a template to create a new container.

The hello-world image creates a really simple container with a short message from Docker specifying the steps that you just ran and more about what's going on behind the scenes including what you just read above. After the output is printed to the terminal, the container exits.

If we run the "docker ps" command, we can see that no containers are currently running:

```
docker ps
```

If we run the "docker ps -a" it will show us our hello-world container that was running but has now exited (see the STATUS column of the output):

```
docker ps -a
```

Docker ps is a command that you will use a lot to view your containers that are currently running.

If you run the "docker info" command again you will see that you have 1 container (in the stopped state) and 1 image downloaded:

```
docker info
```

If you want to see the images that you have on your system, run the "docker images" command:

```
docker images
```

In the output of this command you will see the repository of image names, the tag (which corresponds to the version of the image), the image ID, when it was created and the size of the image.

So to summarize all the information above, here are the commands we looked at.

* docker run - to run a new container
* docker ps - to see running and stopped containers
* docker images - to see info about images stored locally