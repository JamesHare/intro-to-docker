# Scaling Services

Let's think again about desired state vs current state. Desired state is the state (running, paused, stopped, etc) that we want our container to be in. Current state is, as you may have guessed, the current state that the container is in.

If we run the following command, we can see the desired state and current state of our 5 services:

```
docker service ps myservice1
```

By looking at the output, we should be able to see the node id of our 5 services and determine which of our 6 containers does not have a service attached. If we access one of our service containers, and then execute a command to shut it down, we should see the 6th container register as a service to cover the work load. Access any of the service containers and execute the following command:

```
shutdown -h now
```

Next, run the docker service ps myservice1 command again and you should see 5 services still running.

This means that the 6th container picked up the work load automatically because Docker sees that the desired state does not match the current state of the swarm. Which means that Docker Swarm will automatically fix itself, as long as enough containers are running in the swarm to begin with, allowing the DevOps team to be more hands off.

To scale the service to 10 services, we can execute the following command:

```
docker service scale myservice1=10
```

We could give any number as an argument.

We can see the current number of services by executing the following command:

```
docker service ps myservice1
```

In the output, you should see 2 services per node.

It should be noted that if we brought back our node that we shutdown, it will not get automatically added back to the swarm. You will have to go in and add it again as a manager node or a worker node.