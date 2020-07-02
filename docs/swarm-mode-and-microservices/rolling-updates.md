# Rolling Updates

Pushing updates to applications is a fact of life. Rolling updates give us a better way of updating our applications.

Let's start by removing our service that we had previously deployed. We can do that by executing the following command:

```
docker service rm myservice1
```

We can verify that the service instances have all been destroyed by running the following command:

```
docker service ls
```

We should see nothing running in the output, except for the headers.

Next, we want to create a new overlay network for the service. We can do that by executing the following command:

```
docker network create -d overlay my-net
```

To check that the overlay was created successfully, execute the following command:

```
docker network ls
```

Now let's create our service with the following command:

```
docker service create --name myservice2 --network my-net -p 80:80 --replicas 12 [image name]:[version]
```

Running the following command should show that all of our services were created:

```
docker service ps myservice2
```

Next, let's take a look at the service with the inspect command:

```
docker service inspect --pretty myservice2
```

In the output, you will see basic info like the service name, image, ports, etc. and you will also see the update config. This is configuration that we can set when creating the service to instruct Docker on how to handle our rolling updates.

For instance, on the service create command above, we could have also specified the --update-parallelism flag and the --update-deplay flag as shown below:

```
docker service create --name myservice2 --network my-net -p 80:80 --replicas 12 [image name]:[version] --update-parallelism 2 --update-delay 10m
```

The update-paralellism flag tells Docker that you want to update a set of 2 service instances at a time and the update-delay flag tells Docker that you want to wait for 10 minutes between updates.

We can run the update and set the config on the same service by executing the following command:

```
docker service update --image [image name]:[version] --update-parallelism 2 --update-delay 10s myservice2
```

To monitor the rolling update, we can execute the service ps command:

```
docker service ps myservice2
```

After 120 seconds, all 12 of the services will be updated.