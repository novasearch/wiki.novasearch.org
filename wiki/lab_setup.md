---
title: Lab setup
Permalink: wiki/Lab_setup/
layout: wiki
---

Introduction
------------
This guide helps you setting up the required enviroment
- Anaconda
- Conda Environments
- PyTorch + HuggingFace + Spacy + OpenSearch
- JupyterLab
- VSCode or PyCharm
- Final advice


Anaconda (laptop/cluster)
------------

**Step 1: Install Anaconda**

You should install Anaconda in your laptop for programming your models and minimal test. For large-scale testing and training you can use the cluster.

Simply follow the instructions according to your case:

    https://docs.anaconda.com/anaconda/install/


All of the following steps requires you to open the command line interface (CLI) and execute the outlined instructions. To open the terminal to access the command line interface as follows:

 - Linux: press "window key + s", type "terminal", select the terminal application.
 - Windows: press "window key + s", type "Anaconda prompt" (usually "cmd" also works), select the "Anaconda Prompt".
 - Mac: press "command keyh + space", type "terminal", select the terminal application.

Conda Environments
------------

Anaconda allows the creation of Python virtual environments. The main purpose of Python virtual environments is to create an isolated environment for Python projects. This means that each project can have its own dependencies, regardless of what dependencies every other project has.

In Anaconda, virtual environments are referred as conda environments.

PS: Great cheat sheet, covering possible operations for manipulating conda environments and packages: [Cheat Sheet](https://docs.conda.io/projects/conda/en/latest/_downloads/843d9e0198f2a193a3484886fa28163c/conda-cheatsheet.pdf).

**Step 2: Creating conda environments**

Run the following command to create a conda env:

    $ conda create -n nlp-cv-ir python=3.9 ipykernel numpy scipy scikit-learn pandas tqdm jupyter matplotlib gensim flask flask_cors ipympl -c defaults -c conda-forge 

Note that we specified python=3.9 but other python versions are availble to install.

**Step 3: Activate conda environments**

Since you may have multiple conda environemnts, you need to activate the environment in your current shell/terminal:

    $ conda activate nlp-cv-ir


Pycharm or VSCode
------------

Once you have created your Python Environment as described above, you can set up your favourite development environment. PyCharm and VSCode are popular choices offering  different advantages. VSCode is lighter while PyCharm is better for teams. Use your favourite one:
 - [Anaconda + PyCharm](https://docs.anaconda.com/anaconda/user-guide/tasks/pycharm/)
 - [Anaconda + VSCode](https://code.visualstudio.com/docs/python/environments)


PyTorch+HuggingFace+Spacy
------------

The easiest and cleanest way to install PyTorch is through Anaconda. Therefore, first you should create a conda environment (check the latest version of Python supported by PyTorch) and **activate** it.


**Step 1: Install PyTorch**

Go to the [PyTorch website](https://pytorch.org/) and scroll-down to find some sliders that can be used to generated the conda install command.
Choose Linux, Conda and choose the latest CUDA release (11.3 at the moment of writing). Then copy and execute the command. 

Installing on Linux/Windows without GPU:

    $ conda install pytorch torchvision torchaudio cpuonly -c pytorch

Installing on Linux/Windows with GPU:

    $ conda install pytorch torchvision torchaudio pytorch-cuda=12.1 -c pytorch -c nvidia

**NOTE**: If it didn't work, you should check PyTorch guide https://pytorch.org/get-started/locally/ or if you do not have an NVIDIA GPU, install the CPU version instead.

Installing on Mac with CPU-version:

    $  conda install pytorch torchvision torchaudio -c pytorch

**Step 2: Install HuggingFace**

You need to install the following libraries:

    $ pip install transformers
    $ pip install accelerate
    $ pip install ipywidgets
    $ pip install bertviz
    

**Step 3: Install Spacy**

    $ conda install -c conda-forge spacy
    $ python -m spacy download en_core_web_sm

**Step 4: Install Opensearch client**

    $ pip install opensearch-py

**Step 5: Tokenizers**

To install the BPE and WPE tokenizers run this command:

    $ pip install tokenizers


JupyterLab
------------

**Step 1: JupyterHub**

Let's say you have an Anaconda environment called `nlp-cv-ir`. To run things on JupyterHub, you need to install the ipykernel from `nlp-cv-ir`:

1. ```$ conda activate nlp-cv-ir```
2. ```$ python -m ipykernel install --user --name nlp-cv-ir --display-name "nlp-cv-ir" ```

On the command above, you should change the name and display name to the name of your environment.

This creates a new IPython kernel for your env and stores a kernel spec file in:
        
    ~/.local/share/jupyter/kernels/nlp-cv-ir/kernel.json

**Step 2: Start Jupyter Lab locally**

With your environment activated, start jupyter lab in a terminal with the command:

    jupyter lab

For more information about Jupyter Lab visit this [link](https://jupyterlab.readthedocs.io/en/stable/getting_started/overview.html).

**Step 3: Check python version from inside Jupyter/JupyterHub**

 Check which version is running on Jupyter notebook
 
    from platform import python_version
    print(python_version())

 Check version inside your Python program

    import sys
    print(sys.version)

 Check version in command line or shell

    python --version

Final advice
------------
The main advices to ensure everything runs smoothly are the following:
 - Use VSCode or PyCharm as your main **programming enviroment**.
 - Use Jupyter Lab as your main **data and results interactive analysis environment**. Do not program lengthy methods in JupyterLab.
 - Use GIT.
 - Create different environments if you want to "test" some other libraries. Do not damage your main environment.

