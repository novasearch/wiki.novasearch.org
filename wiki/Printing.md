---
title: Printing
permalink: wiki/Printing/
layout: wiki
---

HOWTO: MF411dw
--------------

First download the driver at:
<http://gdlp01.c-wss.com/gds/8/0100007658/05/linux-UFRII-drv-v350-uken.tar.gz>

Extract the archive and install the 64-bit packages:

`   $ cd linux-UFRII-drv-v350-uken/64-bit_Driver/Debian`  
`   $ sudo dpkg -i cndrvcups-ufr2-uk_3.50-1_amd64.deb cndrvcups-common_3.90-1_amd64.deb cndrvcups-utility_1.10-1_amd64.deb`

Take a leap of faith and download another driver at:
<http://files.canon-europe.com/files/soft45505/Software/CQue_v3.0.5_Linux_64_EN.deb>

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

Select Canon -\> MF410
