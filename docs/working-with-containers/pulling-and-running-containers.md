# Pulling and Running Containers

As a quick recap of what we have already looked at in this guide, I wanted to provide more infomration on what is going on behind the scenes when we pull and run containers with Docker.

So we have our "Docker Host" running the docker client and the docker daemon. That combination is also known as the "Docker Engine."

We issue the simple docker run command to the client. The client makes the appropriate API calls to the deamon.

Based on the fact that the client is calling the docker deamon APIs, we can then understnad that the docker deamon implements the Docker Remote API.

After receiving the API call from the client, the docker deamon checks its local store for the image specified in the docker run command. If it does not exist there, the deamon will go and check Docker Hub for the image. [Docker Hub](https://hub.docker.com) is a docker image registery. It's a place where we can store images that we want to use later for contianers. Docker Hub is the default registery that docker will check and it is available on the public Internet. It should be noted that other registeries exist, including secure on-prem registries plus other public and private offerings from third parties. Once the deamon finds the image, it will pull it down to the local machine and then spin up (start) a container using the image.