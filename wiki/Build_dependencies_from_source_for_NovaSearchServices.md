---
title: Build dependencies from source for NovaSearchServices
permalink: wiki/Build_dependencies_from_source_for_NovaSearchServices/
layout: wiki
---

OpenCV 2.4.3
------------

Taken from <http://www.ozbotz.org/opencv-installation/>

<code> sudo add-apt-repository ppa:ubuntu-toolchain-r/test

sudo apt-get update

sudo apt-get install g++-4.7

sudo apt-get remove ffmpeg x264 libx264-dev

sudo apt-get update

sudo apt-get install build-essential checkinstall git cmake libfaac-dev
libjack-jackd2-dev libmp3lame-dev libopencore-amrnb-dev
libopencore-amrwb-dev libsdl1.2-dev libtheora-dev libva-dev libvdpau-dev
libvorbis-dev libx11-dev libxfixes-dev libxvidcore-dev texi2html yasm
zlib1g-dev

sudo apt-get install libgstreamer0.10-0 libgstreamer0.10-dev
gstreamer0.10-tools gstreamer0.10-plugins-base
libgstreamer-plugins-base0.10-dev gstreamer0.10-plugins-good
gstreamer0.10-plugins-ugly gstreamer0.10-plugins-bad
gstreamer0.10-ffmpeg

sudo apt-get install libgtk2.0-0 libgtk2.0-dev

sudo apt-get install libjpeg8 libjpeg8-dev

cd \~

mkdir openCvSrc

cd \~/openCvSrc

wget
<ftp://ftp.videolan.org/pub/videolan/x264/snapshots/x264-snapshot-20121216-2245-stable.tar.bz2le.tar.bz2>

tar xvf x264-snapshot-20121216-2245-stable.tar.bz2

cd x264-snapshot-20121216-2245-stable

./configure --enable-shared --enable-pic

make

sudo make install

cd \~/openCvSrc

wget <http://ffmpeg.org/releases/ffmpeg-0.11.1.tar.bz2>

tar xvf ffmpeg-0.11.1.tar.bz2

cd ffmpeg-0.11.1

./configure --enable-gpl --enable-libfaac --enable-libmp3lame
--enable-libopencore-amrnb --enable-libopencore-amrwb --enable-libtheora
--enable-libvorbis --enable-libx264 --enable-libxvid --enable-nonfree
--enable-postproc --enable-version3 --enable-x11grab --enable-shared
--enable-pic

make

sudo make install

cd \~/openCvSrc

wget
<http://www.linuxtv.org/downloads/v4l-utils/v4l-utils-0.9.3.tar.bz2>

tar xvf v4l-utils-0.9.3.tar.bz2

cd v4l-utils-0.9.3

./configure

make

sudo make install

cd \~/openCvSrc

wget
<http://registrationcenter.intel.com/irc_nas/2563/intel_sdk_for_ocl_applications_2012_x64.tgz>

tar xvf intel\_sdk\_for\_ocl\_applications\_2012\_x64.tgz

sudo apt-get install -y rpm alien libnuma1

sudo alien --to-deb intel\_ocl\_sdk\_2012\_x64.rpm

sudo dpkg -i intel-ocl-sdk\_2.0-31361\_amd64.deb

sudo ln -s /usr/lib64/libOpenCL.so /usr/lib/libOpenCL.so

sudo ldconfig

cd \~/openCvSrc

wget
<http://downloads.sourceforge.net/project/opencvlibrary/opencv-unix/2.4.3/OpenCV-2.4.3.tar.bz2>

tar xvf OpenCV-2.4.3.tar.bz2

cd OpenCV-2.4.3/

mkdir build

cd build

cmake -D CMAKE\_BUILD\_TYPE=RELEASE -DWITH\_OPENCL=ON ..

make

sudo make install

</code>

FFTW
----

<code> cd \~/openCvSrc

wget <http://www.fftw.org/fftw-3.3.3.tar.gz>

tar xvf fftw-3.3.3.tar.gz

cd fftw-3.3.3/

./configure

make

sudo make install

sudo apt-get install fftw3-dev </code>

Armadillo
---------

Extracted from <http://arma.sourceforge.net/download.html>

<code> sudo apt-get install cmake libblas-dev liblapack-dev libboost-dev

wget <http://sourceforge.net/projects/arma/files/armadillo-3.6.1.tar.gz>

tar xvf armadillo-3.6.1.tar.gz

cd armadillo-3.6.1

cmake .

make

sudo make install </code>
