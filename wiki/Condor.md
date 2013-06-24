---
title: Condor
permalink: wiki/Condor/
layout: wiki
---

### Create a submit file

$ vi sim.submit

`   Executable = sim`  
`   Input = sim.in`  
`   Output = sim.out`  
`   Log = sim.log`  
`   queue`

### Submit the job

$ condor\_submit sim.submit
