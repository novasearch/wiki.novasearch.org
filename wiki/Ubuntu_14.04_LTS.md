---
title: Ubuntu 14.04 LTS
permalink: wiki/Ubuntu_14.04_LTS/
layout: wiki
---

### Software

#### Oracle Java

Add the PPA to your package sources with the commands:

`$ sudo add-apt-repository ppa:webupd8team/java`  
`$ sudo apt-get update`

The packages may be installed via package management tools:

`$ sudo apt-get install oracle-java7-installer`  
`$ sudo apt-get install oracle-java8-installer`

#### Zotero Standalone

Add the PPA to your package sources with the commands:

`$ sudo add-apt-repository ppa:smathot/cogscinl`  
`$ sudo apt-get update`

The packages may be installed via package management tools:

`$ sudo apt-get install zotero-standalone`

You probably want to install JabRef also

`$ sudo apt-get install jabref`

#### Sublime Text 3

Add the PPA to your package sources with the commands:

`$ sudo add-apt-repository ppa:webupd8team/sublime-text-3`  
`$ sudo apt-get update`

The packages may be installed via package management tools:

`$ sudo apt-get install sublime-text-installer`

#### X2Go Client

Add the PPA to your package sources with the commands:

`$ sudo apt-add-repository ppa:x2go/stable`  
`$ sudo apt-get update`

The packages may be installed via package management tools:

`$ sudo apt-get install x2goclient`

### Development

#### Build Essential

Sooner or later you have to install this.

`$ sudo apt-get install build-essential`

#### Python Virtualenv

`$ sudo apt-get install python-virtualenv`

If you want to use virtualenvwrapper as well (recommended)

`$ sudo apt-get install virtualenvwrapper`

Then add the following to the bottom of your .bashrc

### Better Power Management

Add the TLP-PPA to your package sources with the commands:

`$ sudo add-apt-repository ppa:linrunner/tlp`  
`$ sudo apt-get update`

The packages may be installed via package management tools:

`$ sudo apt-get install tlp tlp-rdw`

ThinkPads require an additional:

`$ sudo apt-get install tp-smapi-dkms acpi-call-tools`

To see how to configure it yourself check the TLP project configuration
page[1](http://linrunner.de/en/tlp/docs/tlp-configuration.html)

### Tips and Tricks

#### Fix file explorer hangs

Mounting file systems using Nautilus and then suspending/resuming your
session might cause hangs to the file explorer process. If this affects
you, the current best solution is to use this script to automatically
unmount the shares before suspend or hibernate.

</nowiki> }}

#### PulseAudio

Automatically switch to Bluetooth or USB headset by adding the
following:

#### Java Ayatana

Unity global menu and HUD support for Java Swing applications (IntelliJ
IDEA and others).

Add the PPA to your package sources with the commands:

`$ sudo add-apt-repository ppa:danjaredg/jayatana`  
`$ sudo apt-get update`

The packages may be installed via package management tools:

`$ sudo apt-get install jayatana`

#### Alternative font rendering (Infinality patches)

This works very well with the patched OpenJDK.

`$ sudo add-apt-repository ppa:no1wantdthisname/ppa`  
`$ sudo apt-get update`  
`$ sudo apt-get upgrade`  
`$ sudo apt-get install fontconfig-infinality`

Adjust fontconfig files

`$ cd /etc/fonts/infinality/`  
`$ sudo bash infctl.sh setstyle`  
`# select 3) linux`

Change infinality environment variables

`$ sudo nano /etc/profile.d/infinality-settings.sh`  
`# Towards the bottom of the file, there's USE_STYLE.`  
`# USE_STYLE="UBUNTU"`  
`# Logout/Login to take effect`

Change hinting/antialiasing

`$ sudo apt-get install gnome-tweak-tool`  
`$ gnome-tweak-tool`  
`# Go to "Fonts"`  
`# I prefer Full/Rgba`

#### Fix ugly Java/Swing fonts

Some Java apps, and particularly Swing apps such as Intellij IDEA and
Netbeans have terrible font rendering in Linux. To fix that install this
patched OpenJDK and make sure you use it to launch your IDE.

`$ sudo add-apt-repository ppa:no1wantdthisname/openjdk-fontfix`  
`$ sudo apt-get update`  
`$ sudo apt-get install openjdk-7-jdk`

You should also export these environment variables

`$ export JAVA_HOME=/usr/lib/jvm/java-1.7.0-openjdk-amd64`  
`$ export _JAVA_OPTIONS="-Dawt.useSystemAAFontSettings=lcd -Dsun.java2d.xrender=true"`

Prefer this repository (optional)

#### Fix bold fonts

If you have problems with the rendering of text in bold try this

`$ mkdir -p ~/.config/fontconfig/conf.d/`

#### Fix ugly Windows fonts

If you open a document that uses Calibri (or other Windows font) the
rendering will look ugly. To fix it disable embedded bitmap fonts for
your user and let fontconfig use the better Linux rendering with these
fonts.

`$ mkdir -p ~/.config/fontconfig/conf.d/`

#### Zram/Compcache

If you are low on memory you can always compress your data in RAM.

Just issue and check if it works with
