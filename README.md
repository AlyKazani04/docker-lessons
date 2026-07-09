# docker-lessons

### Lesson 1

## What are containers?

- The core of what containers are is just a few features of the Linux kernel duct-taped together to achieve isolation.

## Benefits of a container

- Security and resource-management features of VMs but without the cost of running a whole another OS.

## How they work

- They use chroot, namespaces and cgroups to separate a group of processes from each other.

### chroot

- Stands for 'Change Root'.
- It creates a separate environment for the users so they can't access the files of the host machine.

### Namespaces

- Namespaces allow you to hide processes from other processes.
- So users can't sent signals to other user's processes to sabotage them. (They get separate PIDs(process IDs))

### Cgroups

- Stands for 'Control Groups'.
- This allows us to govern how many resources each of the separate isolated environments can access.
- So no matter how bad a code some user is running, they won't be able to utilize more than, for example, 5% of the CPU.
- This also protects the host machine from resource exhaustion attacks like fork bombs within the containers.

---
