---
title: Condor
permalink: wiki/Condor/
layout: wiki
---

Condor is an workload management system for compute-intensive tasks. It
is used in production environments for more than 15 years, so it is
considered a stable and mature project.

Condor Components
-----------------

-   Job queuing
-   Scheduling policy
-   Priority mechanism
-   Resource monitoring
-   Resource management

Usage
-----

### Create a submit file

$ vi sim.submit

`   Executable = sim`  
`   Input = sim.in`  
`   Output = sim.out`  
`   Log = sim.log`  
`   Queue`

### Submit the job

$ condor\_submit sim.submit

### Watch progress

$ condor\_q

### Running many processes

The real benefit of Condor comes from managing 1000s of jobs.

$ vi sim.submit

`   Executable = sim`  
`   Input = sim.$(PROCESS)`  
`   Output = sim.$(PROCESS)`  
`   Log = sim.log`  
`   Queue 1000`
