# Base Jupyter Lab Server with git based on nVidia CUDA base image

Use this Dockerfile to build your own Docker image to run GPU-accelerated Jupyter Lab

**What's inside:**

* Ubuntu 20.04 runtime with CUDA:11.3
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

docker build -t nvidia_base_conda
......(building)

docker run --gpus all -d -p 8848:8888 --name gpu_conda nvidia_base_conda
38ajcd(container hash)
```

Open your browser, type `http://localhost:8848`, remotely: `http://<yourhostip>:8848`
