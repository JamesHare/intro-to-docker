# What is a Container?

Before containerization became popular in the industry, hypervisors were the go to for running apps.

A hypervisor grabs physical resources like CPU, RAM, Storage and networks. It slices them into virtual components. Virtual CPU, Virtual RAM, etc. Then it builds virtual machines out of them.

Containerization works a bit differently. Instead of slicing the components into virtual components, Docker (and other container engines) slices up Operating System resources. For instance, they slice up the process namespace, the network stack, the storage stack. Every container gets its own Process ID and it's own root file system.

In short, "hypervisor virtualization" virtualizes physical server resources to build virtual machines. Container Engines like Docker use Operating System virtualization. They create virtual Operating Systems and assign one to each container, inside of which we run applications. They are a lot more lightweight than VM's.