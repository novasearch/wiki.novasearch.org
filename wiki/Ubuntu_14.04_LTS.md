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

`$ sudo apt-get install oracle-java7-installer oracle-java7-set-default`

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

#### Videolan 2.1+

Add the PPA to your package sources with the commands:

`$ sudo add-apt-repository ppa:videolan/stable-daily`  
`$ sudo apt-get update`

The packages may be installed via package management tools:

`$ sudo apt-get install vlc`

#### Dropbox

Don't install from the website. Install like this instead:

`$ sudo apt-get install nautilus-dropbox libappindicator1`

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

`$ sudo apt-get install python-pip`  
`$ sudo pip install virtualenv`

If you want to use virtualenvwrapper as well (recommended)

`$ sudo pip install virtualenvwrapper`

Then add the following to the bottom of your .bashrc

### Better Power Management

Add the TLP-PPA to your package sources with the commands:

`$ sudo add-apt-repository ppa:linrunner/tlp`  
`$ sudo apt-get update`

The packages may be installed via package management tools:

`$ sudo apt-get install tlp tlp-rdw`

ThinkPads require an additional:

`$ sudo apt-get install tp-smapi-dkms acpi-call-tools`

Remove default Ubuntu CPU frequency configuration

`$ sudo update-rc.d -f ondemand remove`

To see how to configure it yourself check the TLP project configuration
page[1](http://linrunner.de/en/tlp/docs/tlp-linux-advanced-power-management.html#configuration)

### Tips and Tricks

#### Fix ugly Windows fonts

If you open a document that uses Calibri (or other Windows font) the
rendering will look ugly. To fix it disable embedded bitmap fonts for
your user and let fontconfig use the better Linux rendering with these
fonts.

`$ mkdir ~/.config/fontconfig/conf.d/`
