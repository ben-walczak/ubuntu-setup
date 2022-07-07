# Home Ubuntu Setup

## Introduction

The goal of this repo is to track common installations and themes for my local Ubuntu environment. I've already reinstalled Ubuntu once, so I'm gonna damn well get it right any future tries...

Another goal of this is to finally use my GPU for data science related needs.

## Versions and Links

- https://rapids.ai/start.html#get-rapids
- https://developer.nvidia.com/cuda-11-5-0-download-archive
- https://www.releases.ubuntu.com/20.04/

Check GPU Driver
```bash
ubuntu-drivers devices
```

Versions
```
OS = Linux
Architecture = x86_64
Distribution = Ubuntu
Version = 20.04
Cuda = 11.4
Python 3.9
```

## Installs

Install Docker:
https://docs.docker.com/engine/install/ubuntu/
```bash
sudo apt-get remove docker docker-engine docker.io containerd runc
sudo apt-get update
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

Install Minikube:
```bash
```

Install Cuda Toolkit:
```bash
wget https://developer.download.nvidia.com/compute/cuda/11.4.0/local_installers/cuda_11.4.0_470.42.01_linux.run
sudo sh cuda_11.4.0_470.42.01_linux.run
```

Install Conda:
https://www.digitalocean.com/community/tutorials/how-to-install-the-anaconda-python-distribution-on-ubuntu-20-04
```bash
cd /tmp
curl https://repo.anaconda.com/archive/Anaconda3-2020.02-Linux-x86_64.sh --output anaconda.sh
sha256sum anaconda.sh
bash anaconda.sh
# activate installation in bashrc
source ~/.bashrc
```

Install Rapids:
- https://rapids.ai/start.html#get-rapids
```bash
conda create -n rapids-22.06 -c rapidsai -c nvidia -c conda-forge  \
    cudf=22.06 python=3.9 cudatoolkit=11.4 \
    tensorflow
```

## Bonus Conent

We can also pull Rapids Docker image:
```bash
docker pull rapidsai/rapidsai-core:22.06-cuda11.4-base-ubuntu20.04-py3.9
docker run --gpus all --rm -it \
    --shm-size=1g --ulimit memlock=-1 \
    rapidsai/rapidsai-core:22.06-cuda11.4-base-ubuntu20.04-py3.9
```
I can't imagine how beefy this image is though...

