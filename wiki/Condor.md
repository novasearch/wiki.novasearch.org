---
title: Condor
permalink: wiki/Condor/
layout: wiki
---

Condor is an workload management system for compute-intensive tasks. It
is used in production environments for more than 15 years, so it is
considered a stable and mature project.

Useful commands:
<http://vivaldi.ll.iac.es/sieinvens/siepedia/pmwiki.php?n=HOWTOs.CondorUsefulCommands>

Job submission examples:
<http://vivaldi.ll.iac.es/sieinvens/siepedia/pmwiki.php?n=HOWTOs.CondorSubmitFile>

How to recipes:
<https://htcondor-wiki.cs.wisc.edu/index.cgi/wiki?p=HowToAdminRecipes>

Highlights
----------

-   Preserves user environment on remote machine
-   Users need not make files available or have access to remote machine

Condor Components
-----------------

-   Job queuing
-   Scheduling policy
-   Priority mechanism
-   Resource monitoring
-   Resource management

NovaSeach Condor setup
----------------------

This section details the Condor setup on our cluster.

We have four [nodes](/wiki/Cluster#Hardware "wikilink") with 6 real cores (12
HT threads).

All threads are available for condor, meaning we have 48 Condor slots,
named slot<number>@<machine>.novasearch.org.

### Important information

* To use condor, you must be connected to the head node (zarco). Compute nodes are just workers.

* Each user has a **48GB memory limit** on each machine; each slot has a
**5GB memory limit**.

* You must take these limits into account, so that your jobs don't get
killed as you reach the limit.

Usage
-----

### Create a submit file

	$ vi sim.submit

	Universe = vanilla 
	Executable = sim  
	Output = sim.out  
	Log = sim.log  
	Error = sim.err  
	GetEnv = True 
	Queue

Do not forget "GetEnv" to load your environment!

### Submit the job

$ condor\_submit sim.submit

### Watch progress

$ condor\_q

### Running many processes

The real benefit of Condor comes from managing 1000s of jobs.

	$ vi sim.submit

	Executable = sim  
	getenv = True 
	Input = sim.$(PROCESS) 
	Output = sim.$(PROCESS)
	Log = sim.log 
	Error = sim.err
	Queue 1000

### Running many processes with different arguments

	Executable = sim 
	getenv = True 
	Arguments = $(PROCESS)` 
	Output = sim.$(PROCESS)  
	Log = sim.log  
	Error = sim.err  
	Queue 1000

Will execute 1000 processes with the process id as a parameter: sim 0,
sim 1, sim 2, ... , sim 999

If you need to change multiple arguments, you can set the shared
parameters at the beginning and change the required parameters

	Executable = sim 
	getenv = True 
	Output = sim.$(PROCESS)
	Log = sim.log
	Error = sim.err

	Arguments = a
	Output = a.out
	Queue

	Arguments = b
	Output = b.out
	Queue`  

	Arguments = c 
	Output = c.out 
	Queue

Will execute 3 processes with the selected parameters: sim a, sim b, sim
c and will output to a.out, b.out, c.out respectively.

If you have many parameter combinations, we suggest you generate this
condor file with a script.

### Other useful parameters

	getenv = True

This parameter shares the local environmental variables with the remote
environment. This is useful if you want to share global library paths.

	initialdir = <path>

Sets the base execution path of the execution. Useful to reference files
with relative paths.

	Requirements = (Machine == "compute-0-1.local")

Restricts the job to run on machines that satisfy the requirement. On
this example, the jobs will only be deployed to **compute-0-1**.

### Condor and GPUs

[Here](http://chtc.cs.wisc.edu/gpu-jobs.shtml) you can find information regarding managing GPUs in Condor.

When launching a job, if you need a GPU, you can specify that in your condor submit file with:

	request_GPUs = 1

To check the status of Condor slots and check how many GPUs are in available/in use, you can use `condor_status`:

	$ condor_status -af  Machine Gpus RemoteUser State


### Launching a Python job using *your* Python Environment

You can adapt the following example of a .submit file, to use your Python environment.

Edit a .submit file:

	$ vi example.submit

It should look like this:

	Universe            = vanilla
	Executable          = /home/myusername/.conda/envs/myenv/bin/python
	Arguments           = your_script.py
	getenv              = True
	Transfer_executable = False
	Initialdir          = /home/myusername/             # Point to the base folder of your code (i.e. the your_script.py file)
	Log                 = /home/myusername/condor_test.log.$(PROCESS)
	Output              = /home/myusername/condor_test.out.$(PROCESS)
	Error               = /home/myusername/condor_test.err.$(PROCESS)

	request_GPUs = 1      # If you need a GPU, you must specify it

	Queue 1

The important parts are:
* Executable: It must be the python executable from the environment that you created. If your username is *myusername*, and your environment name is *myenv*, then the path should be */home/myusername/.conda/envs/myenv/bin/python*
* Initialdir: Set this to the path where your code is. It will be your *working directory*.


#### Testing your condor + Python Env setup

Before starting submitting jobs, it is advisable to do a quick test to confirm that everything is working correctly. To do so, create a simple Python script:

	$ touch your_script.py
	$ vi your_script.py

Add the following code to the script:
	
	print("My python script is running!")
	
	# Check if GPUs are seen by PyTorch (if you're not using PyTorch, remove the next two lines)
	import torch
	print("CUDA is available:", torch.cuda.is_available())

Then create a condor .submit file using the one above as example (use your own environment and set each path), and submit it:

	$ condor_submit example.submit
	
Your job is then submitted and the output is now available in the Log file (*/home/myusername/condor_test.out.0*). It should look like this:

	$ cat condor_test.out.0
	My python script is running!
	CUDA is available: True

	
