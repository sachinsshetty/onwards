How to fix - Failed to initialize NVML: Unknown Error

- When you start a nvidia container on docker, you may get
    - $ docker run --rm --runtime=nvidia --gpus all nvidia/cuda:12.6.2-base-ubuntu22.04   nvidia-smi
    - $ Failed to initialize NVML: Unknown Error

- To solve the problem - Follow steps in the link below 
    - https://bobcares.com/blog/docker-failed-to-initialize-nvml-unknown-error/ 

- From the website

How to resolve docker failed to initialize NVML unknown error?

After a random amount of time the GPUs become unavailable inside all the running containers and nvidia-smi returns below error:

“Failed to initialize NVML: Unknown Error”. A restart of all the containers fixes the issue and the GPUs return available.

Today, let us see the methods followed by our support techs to resolve docker error:
Method 1:

1) Kernel parameter
The easiest way to ensure the presence of systemd.unified_cgroup_hierarchy=false param is to check /proc/cmdline :

cat /proc/cmdline

It’s of course related to a method with usage of boot loader. You can hijack this file to set the parameter on runtime

2) nvidia-container configuration
In the file

/etc/nvidia-container-runtime/config.toml

set the parameter

no-cgroups = false

After that restart docker and run test container:

sudo systemctl restart docker
sudo docker run --rm --gpus all nvidia/cuda:11.0-base nvidia-smi
