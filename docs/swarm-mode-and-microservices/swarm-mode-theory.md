# Swarm Mode Theory

## Terms and Concepts

When we talk about **Clusters** we are just talking about **Swarms**, and in the same way when we talk about **Swarms** we are just referring to **Clusters**.

For a more specific explination, a Swarm is a collection of Docker Engines joined into a 
Cluster.

**Swarm Mode** is an entirly optional feature of Docker. Engines that are in a swarm are considered to run in Swarm Mode.

A Cluster running in Swarm Mode will consist of one or more **Manager Nodes** and one or more **Worker Nodes**. 

The **Manager Nodes** maintain the swarm, dispatch tasks and generally look after the state of the Cluster. Manager Nodes are meant to be highly available. The Docker Team recommend 3 - 5 Manager Nodes. Only one Manager Node will be the "leader" or the primary node. If a non-leader receives a request, it will proxy the request over to the leader which will execute it against the swarm. Manager Nodes are also considered Worker Nodes.

The **Worker Nodes** just accept tasks from the Manager Node and execute them.

A **Service** is a declarative way of running and scaling tasks. Say you have a backend and frontend web app. You would have two services. One for the backend and one for the frontend. If you want your app to be highly available, you would need to tell Docker to create replicas of your Services. An example command would be as follows:

```
docker service create --name web-fe --replicas 5 ...
```

This creates 5 intsances (containers) of the service that we defined in the command. If one service dies, there is a reconciliation loop running in the background that will see there is only 4 containers running for the service and it will attempt to start up a new one. The reconciliation loop will continue to make sure that your actual state is the same as your desired state of 5 replicas.

A **Task** is the atomic unit of work assigned to a Worker Node.

To summarize, in a **Swarm**, we have a number of **Manager Nodes** and **Worker Nodes**. We define **Services** and declare them to the Manager Node. The Manager then splits the service into tasks and schedules those tasks against available nodes in the Swarm. In order to deploy complex apps consisting of multiple distributed independently scalable services, we have stacks and distributed application bundles.