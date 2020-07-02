# Services

Services are all about simplifying large scale deployments. We can manage services will the following command:

```
docker service <create | ls | ps | inspect | update| rm>
```

We can start a service with the following command:

```
docker service create --name myservice1 -p 8080:8080 --replicas 5 [image name]
```

If we run the "docker ps" command after running the command above, we will see 5 service instances (or containers).

We can also use the inspect command to get more information about the service:

```
docker service inspect myservice1
```

The most important value we can observe from the inspect command is the network information and endpoints.

If deployed a web app, you will be able to enter any of the endpoints (or ip addresses) of the containers with port 8080 and it shuold serve up your user interface.

The beauty of what we just did, is that we automatically get a fully container aware load balancer. Meaning that no matter what container we hit, we will get our service which will be serving our web app. Docker officially calls this load balancer the "routing mesh."

As you may remember, we have a total of 6 worker nodes in the swarm. Since we asked docker to spin up (or create) 5 replicas of our service, each one will be attached to a worker node (leaving a 6th worker node with nothing attached).