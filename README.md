# Base Jupyter Lab Server with git based on nVidia CUDA base image

Use this Dockerfile to build your own Docker image to run GPU-accelerated Jupyter Lab

Big thanks for the origin author: [gpu-jupyter](https://github.com/iot-salzburg/gpu-jupyter)

**What's inside:**

* Ubuntu 20.04 runtime with CUDA:11.8
* Python 3.8
* Latest Miniconda
* NumPy with Intel MKL accelerated
* Scikit-Learn

For PyTorch, TensorFlow, or other Deep Learning Framework or GPU-accelerated Data Science tools, please feel free to modify `Dockerfile` or install it within the container


**Jupyter Lab Password:**
`gpu-jupyter`

## Step
```shell
git clone https://github.com/JL1829/nvidia_base_notebook.git
cd nvidia_base_notebook

docker build -t <image_name> .

# after build
docker run --gpus all -d -p 8848:8888 --name <container_name> <image_name>
```

For example:

```shell
git clone https://github.com/JL1829/nvidia_base_notebook.git
cd nvidia_base_notebook

docker build -t nvidia_base_conda .
......(building)

docker run --gpus all -d -p 8848:8888 --name gpu_conda nvidia_base_conda
38ajcd(container hash)
```

Open your browser, type `http://localhost:8848`, remotely: `http://<yourhostip>:8848`


## For data persistent and sharing suggesting:
Use [Docker Bind Mount](https://docs.docker.com/storage/bind-mounts/) or [Docker Volume](https://docs.docker.com/storage/volumes/)

### Volume:
* Create Volume first: 
  * `docker volume create myvol` (myvol) is the Volume's name
* Start a container with a Volume
  * `docker run --gpus all -d -p 8848:8888 -v myvol:/home/jovyan/work nvidia_base_conda`
  * (for instant removal) `docker run --gpus all --rm -d -p 8848:8888 -v myvol:/home/jovyan/work nvidia_base_conda`

### Bind Mount:
* Start a container that mounted to your current working directory:
  * `docker run --gpus all -d -p 8848:8888 -v "$(pwd)":/home/jovyan/work nvidia_base_conda`

The container's working directory will have access to your current working directory