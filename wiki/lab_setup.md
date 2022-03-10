---
title: Lab setup
Permalink: wiki/Lab_setup/
layout: wiki
---

Anaconda
------------

**Step 1: Install Anaconda**

Simply follow the instructions according to your case:

    https://docs.anaconda.com/anaconda/install/


All of the following steps requires you to open the command line interface (CLI) and execute the outlined instructions. To open the terminal to access the command line interface as follows:

 - Linux: press "window key + s", type "terminal", select the terminal application.
 - Windows: press "window key + s", type "Anaconda prompt" (usually "cmd" also works), select the "Anaconda Prompt".
 - Mac:

Conda Environments
------------

Anaconda allows the creation of Python virtual environments. The main purpose of Python virtual environments is to create an isolated environment for Python projects. This means that each project can have its own dependencies, regardless of what dependencies every other project has.

In Anaconda, virtual environments are referred as conda environments.

PS: Great cheat sheet, covering possible operations for manipulating conda environments and packages: [Cheat Sheet](https://docs.conda.io/projects/conda/en/latest/_downloads/843d9e0198f2a193a3484886fa28163c/conda-cheatsheet.pdf).

**Step 2: Creating conda environments**

Run the following command to create a conda env:

    $ conda create -n myenv python=3.8 ipykernel numpy scipy scikit-learn pandas tqdm

Note that we specified python=3.8 but other python versions are availble to install.

**Step 3: Activate conda environments**

Since you may have multiple conda environemnts, you need to activate the environment in your current shell:

    $ conda activate myenv


PyTorch+HuggingFace+Spacy
------------

The easiest and cleanest way to install PyTorch is through Anaconda. Therefore, first you should create a conda environment (check the latest version of Python supported by PyTorch) and **activate** it.


**Step 1: Install PyTorch**

Go to the [PyTorch website](https://pytorch.org/) and scroll-down to find some sliders that can be used to generated the conda install command.
Choose Linux, Conda and choose the latest CUDA release (11.1 at the moment of writing). Then copy and execute the command. It should look like:

    $ conda install pytorch torchvision cudatoolkit=11.1 -c pytorch -c nvidia



**Step 2: Install HuggingFace**

First you need to install the following libraries:

    $ pip install transformers
    $ pip install ipywidgets
    $ pip install bertviz

**Step 3: Install Spacy**

    $ conda install -c conda-forge spacy
    $ python -m spacy download en_core_web_sm

**Step 4: Tokenizers**

To install the BPE and WPE tokenizers run this command:

    $ pip install tokenizers

For the BERT tokenizers you need to download one these files and store it in your working directory:

    'bert-base-uncased': "https://s3.amazonaws.com/models.huggingface.co/bert/bert-base-uncased-vocab.txt"

    'bert-large-uncased': "https://s3.amazonaws.com/models.huggingface.co/bert/bert-large-uncased-vocab.txt"

    'bert-base-cased': "https://s3.amazonaws.com/models.huggingface.co/bert/bert-base-cased-vocab.txt"

    'bert-large-cased': "https://s3.amazonaws.com/models.huggingface.co/bert/bert-large-cased-vocab.txt"

    'bert-base-multilingual-uncased': "https://s3.amazonaws.com/models.huggingface.co/bert/bert-base-multilingual-uncased-vocab.txt"

    'bert-base-multilingual-cased': "https://s3.amazonaws.com/models.huggingface.co/bert/bert-base-multilingual-cased-vocab.txt"

    'bert-base-chinese': "https://s3.amazonaws.com/models.huggingface.co/bert/bert-base-chinese-vocab.txt"

    'bert-base-german-cased': "https://int-deepset-models-bert.s3.eu-central-1.amazonaws.com/pytorch/bert-base-german-cased-vocab.txt"

    'bert-large-uncased-whole-word-masking': "https://s3.amazonaws.com/models.huggingface.co/bert/bert-large-uncased-whole-word-masking-vocab.txt"

    'bert-large-cased-whole-word-masking': "https://s3.amazonaws.com/models.huggingface.co/bert/bert-large-cased-whole-word-masking-vocab.txt"

    'bert-large-uncased-whole-word-masking-finetuned-squad': "https://s3.amazonaws.com/models.huggingface.co/bert/bert-large-uncased-whole-word-masking-finetuned-squad-vocab.txt"

    'bert-large-cased-whole-word-masking-finetuned-squad': "https://s3.amazonaws.com/models.huggingface.co/bert/bert-large-cased-whole-word-masking-finetuned-squad-vocab.txt"

    'bert-base-cased-finetuned-mrpc': "https://s3.amazonaws.com/models.huggingface.co/bert/bert-base-cased-finetuned-mrpc-vocab.txt"


Pyserini Environment
--------------------

    $ conda create -n pyserini python=3.8 ipykernel cython numpy scipy scikit-learn pandas tqdm tensorflow
    $ conda activate pyserini
    $ conda install faiss-cpu -c pytorch
    $ pip install pyserini
    $ python -m ipykernel install --user --name pyserini --display-name "Python (pyserini)"
    
Enter this in the first cell of your notebook `%env JAVA_HOME=/share/apps/jdk/jdk-11`


JupyterHub and Conda Environments
------------

**Step 1: JupyterHub**

Let's say you have an Anaconda environment called `myenv`. To run things on JupyterHub, you need to install the ipykernel **from `myenv`**:

1. ```$ conda activate myenv```
2. ```$ python -m ipykernel install --user --name myenv --display-name "Python (myenv)" ```

This creates a new IPython kernel for your env and stores a kernel spec file in:
        
    ~/.local/share/jupyter/kernels/myenv/kernel.json

**Step 2: Check python version from inside JupyterHub**

 Check version runing on Jupyter notebook
 
    from platform import python_version
    print(python_version())

 Check version inside your Python program

    import sys
    print(sys.version)

 Check version in command line or shell
    python --version

