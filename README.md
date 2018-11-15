# TensorRT Tutorial

This projects explores how to install and use TensorRT 5.0.

## 1. Introduction

## 2. Installation

### 2.0 Dependency Analysis

TensorRT depends on the following packages and it is critical to install them 
before installing TensorRT. Most importantly, please ensure the versions of 
these packages are correct because TensorRT has a stringent requirement on them.

1. **Tensorflow** It is recommended to install `1.9.0`, but my tryout of `1.8.0` 
also succeeded.
2. **Python and Python-Dev** `python version == 2.7 or 3.5`. Do not use versions 
higer than 3.5 because 
TensorRT does not support them yet. Therefore, specify which version of python 
or pip you are using when you type command lines. An inappropriate version of
Python would cause the following problem when you run TensorRT
```
ImportError: /usr/local/anaconda3/lib/python3.6/site-packages/tensorrt/tensorrt.so: undefined symbol: _Py_ZeroStruct
```
Install Python-Dev if it has not been installed. An example for Ubuntu
```
sudo apt-get python-dev
```
3. **CUDA** `version==9.0 or 10.0`. If your CUDA version is 9.2, I am sorry you
have to re-install it. Otherwise, you will probably bump into problems like this
when you import TensorRT in your codes:
```
ImportError:libcublas.so.9.0: cannot open shared object file: No such file or directory
```
4. **PyCUDA** `version>=2017.1.1`
5. **cuDNN** `version==7.1.3`
6. **PyTorch [optional]** `version<=0.4.1`

### 2.1 Prerequisites

1. Tensorflow can be simply installed using `pip`.
```
pip3.5 install 'tensorflow-gpu==1.9.0'
```
2. You can check you CUDA version using the following command line if it has been
installed:
```
cat /usr/local/cuda/version.txt
```
If no CUDA exists on you server, follow this [instruction](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html)
to install and download CUDA. Do not forget to set environment variables after 
installation and then source `/etc/profile`. Here is an example for CUDA 9.0
```
export CUDA_HOME="/usr/local/cuda"
export LD_LIBRARY_PATH="/usr/local/cuda-9.0/lib64:$LD_LIBRARY_PATH"
export PATH="/usr/local/cuda-9.0/bin:$PATH"
```
3. Though PyCUDA can be installed by `pip`, but you have to set the 
correct environment variable in the first place in order to ensure the path of 
CUDA available for sudo. Otherwise, you will run into a problem like this
```
src/cpp/cuda.hpp:14:18: fatal error: cuda.h: No such file or directory
compilation terminated.
error: command 'gcc' failed with exit status 1
```
The command line to set path variable is also shown in step 2
```
export PATH=/usr/local/cuda/bin:$PATH
```
Finally, install PyCUDA via `pip`
```
pip3.5 install 'pycuda>=2017.1.1'
```

### 2.2 Download Installation File

Ensure you are a member of the NVIDIA Developer Program. If not, follow the prompts to gain access.
1. Go to: [https://developer.nvidia.com/tensorrt](https://developer.nvidia.com/tensorrt).
2. Click Download.
3. Complete the TensorRT Download Survey.
4. Select the checkbox to agree to the license terms.
5. Click the package you want to install. Your download begins.

There are several downloadable installation files of TensorRT for Linux. Please 
first check your Linux version 
```
cat /etc/issue
```
and CUDA version
```
cat /usr/local/cuda/version.txt
```
Then click the correct link to download TensorRT.

It is possible that your CUDA version is not supported by the current version 
of TensorRT. It happened to me that the CUDA version on my server is `9.2`,
but TensorRT only supports either `9.0` or `10.0`. In this case, one has to 
re-install CUDA. Click [here](http://developer.nvidia.com/cuda-downloads) to 
install the correct version of CUDA on your server.

### 2.3 Install TensorRT

1. Unpack the tar file.
```
$ tar -xvf TensorRT-5.x.x.x.Ubuntu-1x.04.x.x86_64-gnu.cuda-x.x.cudnn7.3.tar.gz
```
Where: 5.x.x.x is your TensorRT version,
Ubuntu-1x.04.x is 14.04.5, 16.04.4 or 18.04.1,
cuda-x.x is the CUDA version 9.0 or 10.0.
This directory will have sub-directories like lib, include, data, etc…
```
$ ls TensorRT-5.x.x.x
bin  data  doc  graphsurgeon  include  lib  python  samples  targets  TensorRT-Release-Notes.pdf  uff
```
2. Add the absolute path to the TensorRT lib directory to the environment variable LD_LIBRARY_PATH:
```
$ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:<eg:TensorRT-5.x.x.x/lib>
```
3. Install the Python TensorRT wheel file.
```
$ cd TensorRT-5.x.x.x/python
$ sudo pip3.5 install tensorrt-5.x.x.x-py2.py3-none-any.whl
```
4. Install the Python UFF wheel file.
```
$ cd TensorRT-5.x.x.x/uff
$ sudo pip3.5 install uff-0.5.1-py2.py3-none-any.whl
```
5. Install the Python graphsurgeon wheel file.
```
$ cd TensorRT-5.x.x.x/graphsurgeon
$ sudo pip3.5 install graphsurgeon-0.2.2-py2.py3-none-any.whl
```

## Appendix

### A.1 Userful Links
* [TensorRT Home Page](https://developer.nvidia.com/tensorrt)
* [TensorRT Introduction](https://devblogs.nvidia.com/tensorrt-3-faster-tensorflow-inference/)
* [TensorRT Installation Guide](https://docs.nvidia.com/deeplearning/sdk/tensorrt-install-guide/index.html#gettingstarted)
* [TensorRT Developer Guide](https://docs.nvidia.com/deeplearning/sdk/tensorrt-developer-guide/index.html#python_topics)
* [CUDA Installation Guide](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html)
* [cuDNN Installation Guide](https://docs.nvidia.com/deeplearning/sdk/cudnn-install/index.html#installcuda)
* [Exporting model from PyTorch to ONNX](https://github.com/onnx/tutorials/blob/master/tutorials/PytorchOnnxExport.ipynb)
