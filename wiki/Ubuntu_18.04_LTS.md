---
title: Ubuntu 18.04 LTS
permalink: wiki/Ubuntu_18.04_LTS/
layout: wiki
---

### Software

#### Java

📖 **Important: Installs OpenJDK Runtime Environment.**

```bash
sudo apt-get install default-jdk
```

#### Sublime Text

Install the GPG key:

```bash
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
```

Add the upstream repository to your package sources with the commands:

```bash
echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
```

The package may be installed via package management tools:

```bash
sudo apt-get update
sudo apt-get install sublime-text
```

### Development

#### Build Essential

Sooner or later you will have to install a C/C++ compiler.

`$ sudo apt-get install build-essential`

#### Python Virtualenv

`$ sudo apt-get install python-virtualenv`

If you want to use virtualenvwrapper as well (recommended)

`$ sudo apt-get install virtualenvwrapper`

Then add the following to the bottom of your `.bashrc`

```bash
if [ -f "$(which virtualenvwrapper_lazy.sh)" ]; then
    . $(which virtualenvwrapper_lazy.sh)
fi
```

Customize the relevant environment variables in `.profile`

```bash
export VIRTUALENVWRAPPER_VIRTUALENV_ARGS='--no-site-packages'
export WORKON_HOME=$HOME/.virtualenvs
export PROJECT_HOME=$HOME/Projects
```

### Better Power Management

Add the TLP-PPA to your package sources with the commands:

`$ sudo add-apt-repository ppa:linrunner/tlp`  
`$ sudo apt-get update`

The packages may be installed via package management tools:

`$ sudo apt-get install tlp tlp-rdw`

To see how to configure it yourself check the TLP project configuration
page[1](http://linrunner.de/en/tlp/docs/tlp-configuration.html)

### Tips and Tricks

#### Fix ugly Windows fonts

If you open a document that uses Calibri (or other Windows font) the
rendering will look ugly. To fix it disable embedded bitmap fonts for
your user and let fontconfig use the better Linux rendering with these
fonts.

Create `~/.config/fontconfig/conf.d/20-no-embedded.conf` with:

```xml
<?xml version='1.0'?>
<!DOCTYPE fontconfig SYSTEM 'fonts.dtd'>
<fontconfig>
 <match target="font">
  <edit mode="assign" name="hinting">
   <bool>false</bool>
  </edit>
 </match>
</fontconfig>
```
