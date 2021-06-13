# openpose-docker
2021-06-13: update the code, fix some bug

A docker build file for CMU openpose with Python API support

https://hub.docker.com/r/cwaffles/openpose

### Requirements
- Nvidia Docker runtime: https://github.com/NVIDIA/nvidia-docker#quickstart
- CUDA 10.0 or higher on your host, check with `nvidia-smi`

### Getting started

#### cloning the repo.(local cmd)
```
$ git clone https://github.com/u0251077/openpose-docker.git
```
#### build the image using dockerfile(local cmd)
```
$ cd ./openpose-docker
$ sudo docker build -t openpose .
```
#### start docker env.(local cmd)
```
$ sudo docker run --gpus all --net host -e DISPLAY=:1 --name openpose_test -it openpose:latest /bin/bash
```

#### build python openpose(docker)
```
$ cd /openpose/build/python/openpose
$ make install
```
#### setup env. for pyopenpose(docker)
```
$ cd /openpose/build/python/openpose
$ cp ./pyopenpose.cpython-36m-x86_64-linux-gnu.so /usr/local/lib/python3.6/dist-packages
$ cd /usr/local/lib/python3.6/dist-packages
$ ln -s pyopenpose.cpython-36m-x86_64-linux-gnu.so pyopenpose
$ export LD_LIBRARY_PATH=/openpose/build/python/openpose
$ python3
>>> import pyopenpose as op
>>> 
```
#### setup x11 in your local cmd(local cmd)
```
$ xhost +
```

#### run examples(docker)
```
# download model
$ cd /openpose/models
$ bash getModels.sh

# test python examples
$ cd /openpose/examples/tutorial_api_python

# please follow this commit to fix code(https://github.com/u0251077/openpose-docker/commit/62dca300d491618448c86ae3043975e753d74429)
# you can use vim to modify the code
$ python3 01_body_from_image.py
```

:+1: (success)

#### result
![](https://i.imgur.com/stkGveW.png)
