---
title: tensorflow 1.4.0 for ubuntu
date: 2017-11-18 11:00:06
tags:
- deep learning package
- nvidia
---

Recently I found that the workstation in my office had a NVIDIA GPU. It is Quodra K620 with 2G memory, so I decided to make it in good use. Here is a note for how to install tensorflow 1.4.0 for ubuntu 16.04 LTS. For tensorflow 1.4.0, I find that CUDA 8.0 and cudnn v6.0 is the most recommended combination.

I maily follow the documents on [official Tensorflow website](https://www.tensorflow.org/install/install_linux#python_36) and some NVIDIA documents.

## Install CUDA Toolkit 8.0

The official documents are very detailed but have too many details. To sum them up, 3 main steps are involved.

### Step1: Pre-installation actions

This is just a pre-check to see whether your computer can install CUDA.

#### Verify You Have a CUDA-Capable GPU

``` bash
$ lspci | grep -i nvidia
```

If it returns nothing, we can give up installing it.

#### Check you have gcc installed

This is for compilation.

``` bash
$ gcc --version
```

#### Remember your architecture

x86_64 or others.

``` bash
$ uname -m && cat /etc/*release
```

### Step2: Download .deb file and install

First I choose a proper .deb to download [here].(https://developer.nvidia.com/cuda-80-ga2-download-archive)
![cuda_1](http://owk4gfyq5.bkt.clouddn.com/cuda_1.png ".deb local file")

Next, we enter the following 3 commands in terminal.

``` bash
sudo dpkg -i cuda-repo-ubuntu1604-8-0-local-ga2_8.0.61-1_amd64.deb
sudo apt-get update
sudo apt-get install cuda
```

### Step3: Post-installing 

Last, change environment variables: add these 2 lines to .bashrc or .zshrc.

``` bash
$ export PATH=/usr/local/cuda-8.0/bin${PATH:+:${PATH}}

$ export LD_LIBRARY_PATH=/usr/local/cuda-8.0/lib64\
                         ${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```

After this, we should check 2 things:

1. If the driver is properly installed by:

``` bash
nvidia-smi # check if driver is properly installed
```

2. Run some samples in `/usr/local/cuda-8.0/samples` to check CUDA.

## Install cudnn v6.0

The cudnn is the nvidia's deep learning library. You can find cudnn v6.0 [here](https://developer.nvidia.com/rdp/cudnn-download) and download `cuDNN v6.0 Library for Linux`.

Then unpack and copy some files to `/usr/local/cuda` directory.

``` bash
tar -zxvf cudnn-8.0-linux-x64-v6.0.tgz
sudo cp cuda/include/cudnn.h /usr/local/cuda/include/
sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64/ -d 
sudo chmod a+r /usr/local/cuda/include/cudnn.h
sudo chmod a+r /usr/local/cuda/lib64/libcudnn*
```
## Install tensorflow-gpu 1.4.0

This the last step before we can use tensorflow.

1. You may need `$ sudo apt-get install libcupti-dev` to install this NVIDIA CUDA Profile Tools Interface.

2. Use `pip3 install tensorflow-gpu` to install the tensorflow gpu version.

## Check with examples

Finally, we can try following codes:

``` python 
# Creates a graph.
a = tf.constant([1.0, 2.0, 3.0, 4.0, 5.0, 6.0], shape=[2, 3], name='a')
b = tf.constant([1.0, 2.0, 3.0, 4.0, 5.0, 6.0], shape=[3, 2], name='b')
c = tf.matmul(a, b)
# Creates a session with log_device_placement set to True.
sess = tf.Session(config=tf.ConfigProto(log_device_placement=True))
# Runs the op.
print(sess.run(c))
```

