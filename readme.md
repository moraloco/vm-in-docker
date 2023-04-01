# Docker Image for Running VM Images

This repository contains a Docker image that can be used to run virtual machine images within a container. The container includes a hypervisor (QEMU-KVM) and allows for running Windows or other operating systems on a Linux host.

This project was inspired by **Abed Samhuri's blog post** and we would like to thank him for his step-by-step instructions.

## Running the Docker Image
To run the docker image, first ensure that your system supports virtualization by running:

```
sudo egrep -c '(vmx|svm)' /proc/cpuinfo
```

If the output is greater than 0, your system supports virtualization. Otherwise, enable virtualization (VT-x) in the BIOS settings or through the virtualization software.

Next, run the following command to start the container:

```
sudo docker run --privileged -it --name <containername> --device=/dev/kvm --device=/dev/net/tun -v /sys/fs/cgroup:/sys/fs/cgroup:rw --cap-add=NET_ADMIN --cap-add=SYS_ADMIN <imagename> bash
```

The container includes the following parameters:

* --privileged: runs the container with root privileges
* -it: starts an interactive terminal
* --name <containername >: assigns a name to the container
* --device=/dev/kvm: maps the device /dev/kvm in the main OS inside the container
* --device=/dev/net/tun: maps the device /dev/net/tun in the main OS inside the container
* -v /sys/fs/cgroup:/sys/fs/cgroup:rw: maps the directory /sys/fs/cgroup in the main OS inside the container with read-write permissions
* --cap-add=NET_ADMIN: adds network admin capabilities to the container
* --cap-add=SYS_ADMIN: adds system admin capabilities to the container
* <imagename>: Choose which of the vm docker images to run
* /bin/bash: starts the container with a bash shell

Finally, to access the Windows VM, install an RDP client for Linux, such as RDesktop:

```
sudo apt-get install rdesktop
```

Note that the Windows Vagrant box includes two built-in accounts:

Username: vagrant, Password: vagrant
Username: Administrator, Password: vagrant

# Acknowledgments

We would like to thank Abed Samhuri for his blog post, which inspired this project. You can read his post [here](https://medium.com/axon-technologies/installing-a-windows-virtual-machine-in-a-linux-docker-container-c78e4c3)