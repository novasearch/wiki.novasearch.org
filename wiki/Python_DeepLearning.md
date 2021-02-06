---
title: Python + Deep Learning Environment Setup
Permalink: wiki/Python_DeepLearning/
layout: wiki
---

Some guidelines/tutorials for installing some common libraries and frameworks in the Rocks Cluster (Work in Progress).


Configuring Anaconda
------------

User Home folders are mounted through nfs. This means you can access your Home folder in the Head node (zarco) and in all the computes (0 to 3), in the exact same path "/home/\<username\>/".

A set of libraries are already ready to use through the "module load" feature. When you need a specific library/software that is not on the cluster, you should compile and install it somewhere on your home folder, such that all the computes can access it.

**Step 1: Add Anaconda to your home init**

Once you first login into your account, you must load one of the Anaconda instalations available on the cluster and configure your bash initialization script:

    $ module load anaconda3/20XX.XX
    $ conda init bash

where XX refers to the version that you select from list available versions on the cluster. Then, you just need to restart your bash shell.

Conda Environments
------------

Anaconda allows the creation of Python virtual environments. The main purpose of Python virtual environments is to create an isolated environment for Python projects. This means that each project can have its own dependencies, regardless of what dependencies every other project has.

In Anaconda, virtual environments are referred as conda environments.

PS: Great cheat sheet, covering possible operations for manipulating conda environments and packages: [Cheat Sheet](https://docs.conda.io/projects/conda/en/latest/_downloads/843d9e0198f2a193a3484886fa28163c/conda-cheatsheet.pdf).

**Step 2: Creating conda environments**

Run the following command to create a conda env:

    $ conda create -n myenv python=3.8 ipykernel

Note that we specified python=3.8 but other python versions are availble to install.

**Step 3: Activate conda environments**

Since you may have multiple conda environemnts, you need to activate the environment in your current shell:

    $ conda activate myenv


PyTorch Environment
------------

The easiest and cleanest way to install PyTorch is through Anaconda. Therefore, first you should create a conda environment (check the latest version of Python supported by PyTorch) and **activate** it.


**Step 4: Install PyTorch**

Go to the [PyTorch website](https://pytorch.org/) and scroll-down to find some sliders that can be used to generated the conda install command.
Choose Linux, Conda and choose the latest CUDA release (10.2 at the moment of writing). Then copy and execute the command. It should look like:

    $ conda install pytorch torchvision cudatoolkit=10.2 -c pytorch
    
**Step 5: JupyterHub and PyTorch**

Let's say you have an Anaconda environment called `myenv`. To run things on JupyterHub, you need to install the ipykernel in that env:

    $ python -m ipykernel install --user --name myenv --display-name "Python (myenv)"

This creates a new IPython kernel for your env and stores a kernel spec file in:
        
    ~/.local/share/jupyter/kernels/myenv/kernel.json


TensorFlow Environment
------------
For the Web Mining and Data Search course, we will need to install at least the following libraries: Numpy, Scipy, IPython, Jupyter, Scikit-learn, Scikit-image, Tensorflow, Keras, NLTK, Gensim and Pandas.

**Step 4: A Conda Environment for Web Data Mining and Search**

Before attempting to install these libraries, make sure have created the conda environment for this course and that you activated it:

    $ conda create -n WebSearch python=3.6
    $ conda activate WebSearch

**Step 5: Installing the required Python libraries**

    $ conda install pip h5py numpy scipy scikit-learn scikit-image gensim nltk jupyter pandas ipykernel

Conda will also install the required libraries’ dependencies.

**Step 6: Installing TensorFlow and Keras**

    $ conda install tensorflow==1.15

If you have an NVIDIA GPU, you can install tensorflow with GPU support. Check TensorFlow documentation for installation instructions for your platform.

    $ conda install keras

In the above command, conda will select the keras version that is suited to your version of TensorFlow.

**Step 7: Setup Keras to use TensorFlow backend**

Create a Keras config file -  Linux and macOS:

    $ mkdir ~/keras && touch ~/keras/keras.json

Open the created file and paste:

    {
        "floatx": "float32",
        "epsilon": 1e-07,
        "backend": "tensorflow",
        "image_data_format": "channels_last"
    }

Save and exit.

**Step 8: Keras-TensorFlow integration**

To test if Keras is using the TensorFlow backend you can run:

    $ python
    $ >>> import keras

It should print the following message: Using TensorFlow backend.

**Step 9: JupyterHub**

Create a Jupyter Kernel in your conda environment

To create a JupyterHub Kernel with currently active environment you need to do this:

    $ ipython kernel install --user --name=WebSearch

Note that the name above can be different from the current environment name. 

**Step 10: Deactivate the conda environment**

Now you should deactivate the conda environment to avoid changing its configuration:

    $ conda deactivate


Pyserini Environment
--------------------

    $ conda create -n pyserini python=3.8 ipykernel cython numpy scipy scikit-learn pandas tqdm tensorflow
    $ conda activate pyserini
    $ conda install faiss-cpu -c pytorch
    $ pip install pyserini
    $ python -m ipykernel install --user --name pyserini --display-name "Python (pyserini)"
    
Enter this in the first cell of your notebook `%env JAVA_HOME=/share/apps/jdk/jdk-11`
