---
title: IR + NLP lab setup
Permalink: wiki/Lab_setup/
layout: wiki
---

Install Anaconda
------------

**Step 1: Install Anaconda**



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
    

Spacy
--------------------

**Step 5: Install Spacy and its models**



Pyserini Environment
--------------------

**Step 6: Install Pyserini**


    $ conda create -n pyserini python=3.8 ipykernel cython numpy scipy scikit-learn pandas tqdm tensorflow
    $ conda activate pyserini
    $ conda install faiss-cpu -c pytorch
    $ pip install pyserini
    $ python -m ipykernel install --user --name pyserini --display-name "Python (pyserini)"
    
Enter this in the first cell of your notebook `%env JAVA_HOME=/share/apps/jdk/jdk-11`


JupyterHub and PyTorch
------------

**Step 7: JupyterHub and PyTorch**

Let's say you have an Anaconda environment called `myenv`. To run things on JupyterHub, you need to install the ipykernel **from `myenv`**:

1. ```$ conda activate myenv```
2. ```$ python -m ipykernel install --user --name myenv --display-name "Python (myenv)" ```

This creates a new IPython kernel for your env and stores a kernel spec file in:
        
    ~/.local/share/jupyter/kernels/myenv/kernel.json

**Step 8: Check python version from inside JupyterHub**

 Check version runing on Jupyter notebook
 
    from platform import python_version
    print(python_version())

 Check version inside your Python program

    import sys
    print(sys.version)

 Check version in command line or shell
    python --version

