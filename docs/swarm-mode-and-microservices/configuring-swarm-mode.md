# Configuring Swarm Mode

To build a Swarm with 3 Manager Nodes and 3 Worker Nodes, we will start by executing docker run for 6 containers. These containers can be anything, but should probably just be bare-metal Linux containers for now. We can use the official Ubuntu image from Docker Hub.

```
docker run -d --name [mgr-1] ubuntu
```

Make sure to change the name for each of the containers. When you have 3 contianers running named wrk (worker) and 3 containers named mgr (manager), continue below.

Let's initialize the swarm by getting into the mgr-1 container.

Once in the first manager container, execute the following command to initialize the swarm:

```
docker swarm init --advertise-addr 192.168.1.5:2377 --listen-addr 192.168.1.5:2377
```

The **--advertise-addr** flag lets Docker know that this is the address that we want it to use for swarm related work.

The **--listen-addr** flag lets Docker know that this is the address we want is to listen on for Swarm manager traffic.

The ip address has to be valid on your network and should always be the address of the node that you are on. You can use any port that is in your environemnt. However, 2377 is considered the official Swarm port.

After execution is complete, a new command will be printed to the console to execute on the Worker Nodes to allow them to join the swarm. Copy this and remember it for later.

While we are still on the mgr-1 node, execute the following two commands and observe the output:

```
docker swarm join-token manager
```

```
docker swarm join-token worker
```

The output of these two commands will give a much longer command that you should execute on all your manager nodes and worker nodes respectively. Docker will be able to tell which is a manager and which is a worker by the last part of the token given on the --token flag.

If we want to verify that the swarm has been initialized properly, we can execute the following command:

```
docker info
```

In the output, you will see information about the current swarm.

As a side note, if you ever have a worker node that you want to promote to a manager node, you can execute the following command on that worker node:

```
docker node promote [container id]
```