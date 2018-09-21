---
title: Printing
permalink: wiki/Printing/
layout: wiki
---

HOWTO: MF411dw
--------------

First, take a leap of faith and download the driver at:
<http://files.canon-europe.com/files/soft45505/Driver/CQue_v4.0.0_Linux_64_EN.deb>

We need to create the following link so the filter can be found on the
path!

`   $ sudo ln -s /opt/cel/bin/sicgsfilter /bin/sicgsfilter`

Without this all your printing jobs will fail due to "Filter Failed"
like shown below:

`   D [08/Jun/2018:14:50:40 +0100] [Job 95] /bin/sh: 1: sicgsfilter: not found`  
`   D [08/Jun/2018:14:50:40 +0100] [Job 95] renderer exited with status 127`  
`   D [08/Jun/2018:14:50:40 +0100] [Job 95] Process is dying with \"Encountered error Broken pipe during fwrite\", exit stat 1`  
`   D [08/Jun/2018:14:50:40 +0100] [Job 95] Cleaning up...`  
`   D [08/Jun/2018:14:50:40 +0100] [Job 95] Killing pdf-to-ps`

We will need the full address of a printer. For convenience here is the
address of one:

`   `[`ipp://print.ci.fct.unl.pt:631/printers/di-canon-MF411DW-piso3`](ipp://print.ci.fct.unl.pt:631/printers/di-canon-MF411DW-piso3)

Select Canon MF411dw/416dw **PCL**

Don't forget to also install the Papercut client:
<http://ftp.ci.fct.unl.pt/publico/Papercut/v18.1.4/>
