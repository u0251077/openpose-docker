# openpose-docker
2021-06-13: update the code, fix some bug

A docker build file for CMU openpose with Python API support

https://hub.docker.com/r/cwaffles/openpose

### Requirements
- Nvidia Docker runtime: https://github.com/NVIDIA/nvidia-docker#quickstart
- CUDA 10.0 or higher on your host, check with `nvidia-smi`

### Getting started

#### cloning the repo.
```
$ git clone https://github.com/u0251077/openpose-docker.git
```
#### build the image using dockerfile
```
$ cd ./openpose-docker
$ sudo docker build -t openpose .
```
#### start docker env.
```
$ sudo docker run --gpus all --net host -e DISPLAY=:1 --name openpose_test -it openpose:latest /bin/bash
```

#### build python openpose
```
$ cd /openpose/build/python/openpose
$ make install
```
#### setup env. for pyopenpose
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
#### setup x11 in your local cmd
```
$ xhost +
```

#### run examples
```
# download model
$ cd /openpose/models
$ bash getModels.sh

# test python examples
$ cd /openpose/examples/tutorial_api_python

# please follow this commit to fix code(https://github.com/u0251077/openpose-docker/commit/2e304a7997c41d287386f12c4ec80281d8c107bc)
# you can use vim to modify the code
$ python3 01_body_from_image.py
```

:+1: (success)

#### result
![](https://i.imgur.com/stkGveW.png)
