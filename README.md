## All-in-one Docker image with common machine learning tools
Here are Dockerfiles to get you up and running with a fully functional deep learning machine. It contains all the popular deep learning frameworks with CPU and GPU support (CUDA and cuDNN included). The CPU version should work on Linux, Windows and OS X. The GPU version will, however, only work on Linux machines. See [OS support](#what-operating-systems-are-supported) for details

## Setup
### Prerequisites
1. Install Docker following the installation guide for your platform: [https://docs.docker.com/engine/installation/](https://docs.docker.com/engine/installation/)

2. **GPU Version Only**: Install Nvidia drivers on your machine either from [Nvidia](http://www.nvidia.com/Download/index.aspx?lang=en-us) directly or follow the instructions [here](https://github.com/saiprashanths/dl-setup#nvidia-drivers). Note that you _don't_ have to install CUDA or cuDNN. These are included in the Docker container.

3. **GPU Version Only**: Install nvidia-docker: [https://github.com/NVIDIA/nvidia-docker](https://github.com/NVIDIA/nvidia-docker), following the instructions [here](https://github.com/NVIDIA/nvidia-docker/wiki/Installation). This will install a replacement for the docker CLI. It takes care of setting up the Nvidia host driver environment inside the Docker containers and a few other things.

## Common used docker commands
### Clean up container
```bash
docker container ps -a
docker container rm 69b8da54bc43
```

### Remove images
```bash
docker rmi 69b8da54bc43
```

### Download dock files
```bash
git clone https://github.com/zhenliu/dl-docker
```
### Builder docker image
```bash
docker build -t zhenliu/dl-docker:cpu -f Dockerfile.cpu .
```
### start docker container with ipython port
```bash
docker run -it -p 8888:8888 -p 6006:6006 -v ~/dl_root:/root/dl_root zhenliu/dl-docker:cpu bash
```

### start an existing container after machine was reboot
```bash
docker start d3b7d7463857
```

### start an interactive shell to an existing container
```bash
docker exec -it d3b7d7463857 /bin/bash
```

### export the current container into a different image
```bash
docker export -o /home/zhenliu/myfile.tar d3b7d7463857
```
### Import the image. Make sure the same image does not exist.
```bash
docker import /home/qisun/myfile.tar
```
### Execute command in background in docker
```bash
docker exec d3b7d7463857 /bin/bash -c "bwa aln mydata >& log" &
```
### Check the status of the execution
```bash
docker exec d3b7d7463857 ps -ef
```
### Clean all idle containers
```bash
docker container prune
```
