---
title: Installing Software
permalink: wiki/Installing_Software/
layout: wiki
---

WORK IN PROGRESS: Some guidelines/tutorials for software installation in
the Rocks Cluster.

Python Stuff
------------

### General Advice

Compute nodes have a set of useful libraries installed like numpy,
scipy, pandas, etc... The pip tool, which allows one to easily install
new libraries and is also available. It may be used to install any
python library from the Python Package Index or from a git repository.
Example of a command to install a package/library:

`pip install `<package_name>

Since we are simple peasants on the cluster and we don't have sudo (it
makes a lot of sense :)) we need to install libraries locally. To
achieve this, one option is to add the option `--user` to the pip
install command:

`pip install `<package_name>` --user`

For more info see:
[1](http://pip-python3.readthedocs.org/en/latest/user_guide.html#user-installs)

To upgrade a library we specify the argument `--upgrade`, like this:

`pip install --upgrade `<package_name>` --user`

### Machine Learning General Packages

#### Scipy

The Scipy package[2](https://www.scipy.org/) provides a collection of
mathematics, science, and engineering related libraries. It includes
packages like numpy, matplotlib,pandas, ipython, among others.

As any other package, Scipy can be installed by issuing the command:

`pip install --upgrade scipy --user`

However, it is likely that it will fail due to the fact that python
isn't able to find a BLAS library. Since our cluster Rocks, we have MKL
from Intel! To use it, we need to load it and tell pip which MKL version
we wan't numpy to use.

To load mkl on the cluster:

`module load mkl` (confirm if lapack is needed!)

-   Create a configuration file for numpy named `.numpy-site.cfg` in the
    $HOME folder:

  
  
`touch /home/dsemedo/.numpy-site.cfg`

-   Copy the contents of a sample numpy config file available at
    [3](https://github.com/numpy/numpy/blob/master/site.cfg.example) to
    the created file.

Change the MKL section to:

`# MKL`  
`# ----`  
`# MKL is Intel's very optimized yet proprietary implementation of BLAS and`  
`# Lapack.`  
`# For recent (9.0.21, for example) mkl, you need to change the names of the`  
`# lapack library. Assuming you installed the mkl in /opt, for a 32 bits cpu:`  
`[mkl]`  
`library_dirs = /opt/intel/composer_xe_2013_sp1.2.144/mkl/lib/intel64 `  
`include_dirs = /opt/intel/composer_xe_2013_sp1.2.144/mkl/include`  
`mkl_libs = mkl_rt`

After this, Scipy installs correctly and MKL is used in Numpy.

#### scikit-learn

`pip install --upgrade scikit-learn --user`

### Deep Learning Packages

#### Theano

Theano is a Python library that allows the definition, optimization, and
evaluation of mathematical expressions involving multi-dimensional
arrays efficiently.

Install the latest version of Theano using the git repository:

`pip install --upgrade `[`https://github.com/Theano/Theano/archive/master.zip`](https://github.com/Theano/Theano/archive/master.zip)` --user`

Theano supports CPU and GPU. To select which we want to use the Theano
flags must be set:

-   Setting the flags for each execution:

  
  
<code>THEANO\_FLAGS='floatX=float32,device=gpu0' python

<script>

.py</code>

-   Alternatively we can create a config file:

  
  
`echo -e "[global]\nfloatX=float32\ndevice = gpu0\n" > ~/.theanorc`

With this config, Theano will attempt to use the GPU for computations.
If it fails to find a GPU, it will fallback to the CPU.

Additionally, we want Theano to also use MKL:

-   Modify Theano config file by adding:

`[blas]`  
`ldflags = -L/opt/intel/composer_xe_2013_sp1.2.144/mkl/lib/intel64 -L/opt/intel/composer_xe_2013_sp1.2.144/compiler/lib/intel64 -lmkl_gf_lp64 -lmkl_intel_lp64 -lmkl_intel_thread -lmkl_gnu_thread -lmkl_core -lmkl_vml_avx -lmkl_def -ldl -lpthread -lm -lmkl_rt -liomp5`

For more info about Theano flags
see[4](http://deeplearning.net/software/theano/library/config.html).

#### Lasagne

Lasagne is a lightweight library to build and train neural networks in
Theano. It depends on Theano, therefore it must be installed first. To
install Lasagne:

`pip install --upgrade `[`https://github.com/Lasagne/Lasagne/archive/master.zip`](https://github.com/Lasagne/Lasagne/archive/master.zip)` --user`

Lasagne documentation:
[5](http://lasagne.readthedocs.org/en/latest/index.html)

#### Keras

"Keras is a minimalist, highly modular neural networks library, written
in Python and capable of running on top of either TensorFlow or Theano.
It was developed with a focus on enabling fast experimentation. Being
able to go from idea to result with the least possible delay is key to
doing good research."

Dependencies:

-   cv2 -\> `pip install cv2 --user`

`pip install git+git://github.com/Theano/Theano.git --user`

Keras Documentation: [6](http://keras.io/)

### Computer Vision Packages

#### scikit-image

`pip install --upgrade scikit-image --user`

OpenCV
------

Steps for installing OpenCV 3.1.0 with extra modules (OpenCV contrib).
OpenCV will be compiled with support for OpenCL, CUDA and MKL.

Downloading OpenCV: [7](http://opencv.org/downloads.html)

Extra modules must be downloaded from git.

`$ git clone `[`https://github.com/Itseez/opencv_contrib`](https://github.com/Itseez/opencv_contrib)

From now on, let <opencv_contrib_dir> be the the downloaded
opencv\_contrib folder.

Load necessary modules:

`$ module load cmake gnutools mkl python eigen hdf5`

Compiling OpenCV:

`$ cd `<opencv_source>  
`$ mkdir build && cd "$_"`  
`$ cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=`<install_folder>` -D INSTALL_C_EXAMPLES=OFF -D INSTALL_PYTHON_EXAMPLES=ON -D OPENCV_EXTRA_MODULES_PATH=`<opencv_contrib_dir>`/modules -D BUILD_EXAMPLES=ON -D ENABLE_FAST_MATH=1 -D CUDA_FAST_MATH=1 -D WITH_OPENCL=ON -D BUILD_opencv_python2=ON -D PYTHON_INCLUDE_DIR=/opt/python/include/python2.7 -D PYTHON_LIBRARY=/opt/python/lib/libpython2.7.so  ..`  
`$ make -j12`  
`$ make install`

The final step is to add the path of cv2.so library to the PYTHONPATH
variable, such that python finds it:

`# Add this line to ~/.bashrc`  
`export PYTHONPATH=$HOME/opencv_build/lib/python2.7/site-packages:$PYTHONPATH`

To check if it installed correctly:

`$ python`  
`>>> import cv2`

If the import succeeds then Python-OpenCV is installed.

#### Adding support for FFmpeg

Assuming that FFmpeg was compiled previously and the build directory is
<ffmpeg_build>, the following environment variables must be set:

`export LD_LIBRARY_PATH=`<ffmpeg_build>`/lib/:$LD_LIBRARY_PATH`  
`export PKG_CONFIG_PATH=$PKG_CONFIG_PATH:`<ffmpeg_build>`/lib/pkgconfig`  
`export PKG_CONFIG_LIBDIR=$PKG_CONFIG_LIBDIR:`<ffmpeg_build>`/lib/`

Now, cmake should be able to find FFmpeg.

NOTE: FFmpeg must be compiled with the following options:
`./configure --enable-nonfree --enable-pic --enable-shared`

### Common Problems

#### IPPICV hash mismatch

While creating the makefile for compilation, the lib ippicv will be
automatically downloaded. However, the md5sum of the downloaded file
will not match the hardcoded hash on the cmake.

Instead of changing cmake we can manually download the file. Download
URL:
[8](https://raw.githubusercontent.com/Itseez/opencv_3rdparty/81a676001ca8075ada498583e4166079e5744668/ippicv/ippicv_linux_20151201.tgz)
Steps:

`$ mkdir `<opencv_source>`/3rdparty/ippicv/downloads/linux-808b791a6eac9ed78d32a7666804320e && cd "$_"`  
`$ wget `[`https://raw.githubusercontent.com/Itseez/opencv_3rdparty/81a676001ca8075ada498583e4166079e5744668/ippicv/ippicv_linux_20151201.tgz`](https://raw.githubusercontent.com/Itseez/opencv_3rdparty/81a676001ca8075ada498583e4166079e5744668/ippicv/ippicv_linux_20151201.tgz)  
`$ cd ../../ && mkdir unpack && cd "$_"`  
`$ cp ../downloads/linux-808b791a6eac9ed78d32a7666804320e/ippicv_linux_20151201.tgz .`  
`$ tar zxvf ippicv_linux_20151201.tgz`

Alternatively, one can pass the option `-D WITH_IPP=OFF` to the cmake
call to compile without the IPPICV lib.
