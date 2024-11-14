# Linux: start from scratch

Linux is a family of open source Unix-like operating systems based on
the Linux kernel, an operating system kernel first released on September
17, 1991 by Linus Torvalds
([Wikipedia](https://en.wikipedia.org/wiki/Linux)). Linux is typically
packaged in Linux distributions (see
[here](https://en.wikipedia.org/wiki/Linux_distribution)) which include
the Linux kernel and supporting system software and libraries. Ubuntu is
an open source and popular Linux distribution based on Debian. This
article shows how to install and update Ubuntu distribution and provides
a quick reference of helpful shortcuts, applications, and tips for
software installation.

------------------------------------------------------------------------

## Running Ubuntu

The [Ubuntu desktop](https://www.ubuntu.com/desktop) is easy to use,
easy to install and includes everything you need to run your
organisation, school, home or enterprise. It’s also open source, secure
and accessible Linux distribution.

### Create a bootable USB stick

We can test Ubuntu desktop experience without installing it on a PC and
only by installing Ubuntu on a 4 GB or larger flash drive. To create a
bootable USB stick from Windows follow the instruction in
[here](https://tutorials.ubuntu.com/tutorial/tutorial-create-a-usb-stick-on-windows#0)
and from Apple macOS follow the steps in
[here](https://tutorials.ubuntu.com/tutorial/tutorial-create-a-usb-stick-on-macos#0).

### Install Ubuntu desktop

We can install Ubuntu alongside your operating system or delete your
existing operating system and replace it with Ubuntu. To install Ubuntu
desktop follow the instruction
[here](https://tutorials.ubuntu.com/tutorial/tutorial-install-ubuntu-desktop#0).
After installation, use Software Updater application to update Ubuntu.
Note that usually there are two versions of Ubuntu available, first a
long-term support (LTS) version and second the latest version of the
Ubuntu operating system. As a regular user it is better to download the
latest version.

### Advanced Packaging Toolkit

Advanced Packaging Toolkit (APT) is Debian package manager. To update
packages we can use the following commands at a terminal prompt:

``` bash
sudo apt update
sudo apt upgrade
```

To remove cache files:

``` bash
sudo apt autoremove
sudo apt autoclean
```

To install and remove a package:

``` bash
sudo apt install PackageName
sudo apt remove PackageName
```

If some Ubuntu desktop packages were accidentally removed, you may try
installing them by:

``` bash
sudo apt install ubuntu-desktop
```

The following is the list of options:

- `-h, --help`: show a short help
- `-v, --version`: show the program version
- `-c, --config-file`: configuration file; specify a configuration file
  to use
- `-o, --option`: set a configuration option; this will set an arbitrary
  configuration option

For more help, use `apt -h`.

### Useful keyboard shortcuts

The following keyboard shortcuts can be very helpful to use your desktop
and applications more efficiently.

- Activities: `super` (windows/command key)
- Change tabs: `super + tab`
- Change tab’s positions: `super + arrow keys`
- Switch between workspaces: `super + pg dn/pg up`
- Change keyboard language: `super + space`
- Minimize: `super + h`
- Desktop: `super + d`
- Lock screen: `super + l`
- Applications: `super + a`
- Messages: `super + m`
- Favorites app number: `super + q`
- Open the favorite app: `super + 1/2/3/...`
- Close the window: `alt + f4`
  <!-- - unmaximize the window: `alt + f5` -->
  <!-- - maximize the window: `alt + f10` -->
- Terminal prompt: `ctrl + alt + t`
- Top bar: `ctrl + alt + tab`
- Screenshot: `prt sc`

### Ubuntu Software

Ubuntu Software is an small App Store including many useful software and
packages. Following are some popular software available in Ubuntu
Software:

- Slack
- Skype
- Tweaks
- GParted
- GNU Octave
- Sublime Text
- Synaptic Package Manager

### The Unix Shell

The Shell is a program which uses command-line interface, instead of
graphical user interfaces (GUI), to run other programs rather than doing
calculations itself. The most popular Unix Shell is Bash which is
accessible by `ctrl+alt+t` keyboard shortcut in Ubuntu. You may find
more information [here](shell.html).

### Remote connections

Remmina is the default remote desktop client in Ubuntu that supports
Remote Desktop Protocol (RDP) and Virtual Network Computing (VNC) to
access other Windows and Linux computers with graphical interfaces.
[RealVNC](https://www.realvnc.com/en/connect/) also is a good
alternative for VNC remote access that you might look.

For a SSH connection we can easily use this command at a terminal prompt
(use your own user name and remote host address):

``` bash
ssh username@remotehost
```

We can also use an IP address instead of the remote host address in the
above command. To find the host IP address, use `ip a | grep inet` at a
terminal prompt of the host computer.

If you are going to connect to another Linux computer through SSH, make
sure OpenSSH Server client is installed on the host computer. To install
the OpenSSH client, use this command at a terminal prompt of the host
computer:

``` bash
sudo apt install openssh-server
```

We can use X server for remotely displaying applications through SSH.
Use this command at a terminal prompt:

``` bash
ssh -X username@remotehost
```

To display the application simply run it at the terminal prompt. For
example:

``` bash
xclock # Display the server clock
xeyes # Display a pair of eyes!
nautilus # Display Files
google-chrome # Display Chrome browser (if installed)
rstudio # Display RStudio (if installed)
spyder # Display Spyder (if installed)
```

When using slower links the data can be compressed using the -C flag:

``` bash
ssh -XC username@remotehost
```

### Online accounts

We can add online accounts such as Google, Microsoft, and MS Exchange
accounts to `Settings > Online Account`. For Microsoft Exchange account
we need the following information:

- Email: user@mail.missouri.edu
- Password: user password
- Username: user@mail.missouri.edu
- Server: **outlook.office365.com**

To be able to see MS Exchange calender and emails, you may install
Evolution which is an integrated mail, calendar, tasks and contact
management application for Ubuntu. Use this command at a terminal
prompt:

``` bash
sudo apt install evolution-ews
```

If you already have Evolution installed, you might need to kill and
restart Evolution to see MS exchange mails and calender. Use these
commands at a terminal prompt:

``` bash
rm -rf .config/evolution/ .cache/evolution/ .local/share/evolution/
pkill evolution
```

### Local mirror

To get the best download speed when updating software, we can use the
closest mirror to our location. To change mirror settings, go to
`Software & Updates`, click `Ubuntu Software` tab and click
`Download from` and choose `Other` and then choose `Selsect Best Server`
option to find the best available server.

### Disable screen rotation

We can disable screen rotation by using:

``` bash
sudo apt remove iio-sensor-proxy
```

To re-enable the feature, simply run:

``` bash
sudo apt install iio-sensor-proxy
```

### Hide icons

To hide an icon from the application menu, go to
`/usr/share/applications/` and add the following line to
`app_name.desktop`:

``` text
NoDisplay=true
```

For example use `sudo nano /usr/share/applications/R.desktop` to open
the desktop file and add the above line to hide R icon from the menu.

To hide Trash or Home from Desktop use:

``` bash
gsettings set org.gnome.nautilus.desktop trash-icon-visible false

# In Ubuntu 19.04
gsettings set org.gnome.shell.extensions.desktop-icons show-trash false
gsettings set org.gnome.shell.extensions.desktop-icons show-home false
```

We can return Trash and Home back to Desktop by setting `true` for the
above commands.

### GRUB menu

To see GRUB menu at boot-time, open `/etc/default/grub` file and change
`GRUB_TIMEOUT` from 0 seconds to 5 seconds. Save changes and run
`sudo update-grub` to apply changes.

------------------------------------------------------------------------

## Software installation

Most of the software that are available for Windows and macOS are
available for Linux. Also, usually there is a great alternative for
software that are not available. For example, sf package in R is a great
alternative for ArcGIS Desktop that is not available for Linux. The
following provides helpful tips to install some software in Ubuntu.

### Chrome

Chrome is available [here](https://www.google.com/chrome/) to download.
Useful Chrome keyboard shortcuts are listed in below.

- New tab: `ctrl + t`
- Close tab: `ctrl + w`
- Change tab: `ctrl + tab`
- New window: `ctrl + n`
- History: `ctrl + h`
- Add to favorites: `ctrl + d`

### Git

To install Git, use:

``` bash
sudo apt install git
```

You may learn more about Git [here](git.html).

### Emacs

Emacs is a powerful text editor. Use the following to install Emacs:

``` bash
sudo apt install emacs
```

You may learn more about Emacs [here](emacs.html).

### Python

Python should be installed on your system. Enter `python3` in the
terminal to open Python.

### Conda

[Conda](https://docs.conda.io/projects/conda/en/latest/) is an open
source package management system and environment management system.
Conda quickly installs, runs and updates packages and their
dependencies. Conda easily creates, saves, loads, and switches between
environments on your local computer. It was created for Python programs
but it can package and distribute software for any language.

Download Miniconda from
[here](https://docs.conda.io/en/latest/miniconda.html) for using Conda.
After downloading the installer, enter the following command at a
terminal prompt to install Miniconda.

``` bash
bash ~/Downloads/Miniconda3-latest-Linux-x86_64.sh
```

Follow the instruction to complete the installation. Run the following
to prevent Conda to activate as base by default:

``` bash
conda config --set auto_activate_base false`
```

To update Conda and update/install/remove other packages use:

``` bash
conda update conda
conda update/install/remove <pkg_name> 
```

To remove Miniconda, use:

``` bash
rm -rf ~/miniconda3
rm -rf ~/.condarc ~/.conda ~/.continuum
```

Anaconda, the heavier version of Miniconda which includes Conda and many
other Python/R data science packages, is available
[here](https://www.anaconda.com/distribution/#linux). After download,
install Anaconda by:

``` bash
bash ~/Downloads/Anaconda3-x.x.x-Linux-x86_64.sh
```

To update Anaconda use:

``` bash
conda update conda
conda update anaconda 
```

And to remove Anaconda run:

``` bash
conda install anaconda-clean
anaconda-clean --yes
rm -rf ~/anaconda3
```

To learn more about managing environments by Conda see the instruction
in [here](python_env.html#miniconda).

### R

We can use APT package manger to download R by:

``` bash
apt install r-base-core
```

Note that APT might has an old version of R. It is better to check R
version before installing by `apt-cache policy r-base-core`. If R
version is very outdated, then to obtain the latest R, follow the
instruction at [R website](https://cran.r-project.org/bin/linux/ubuntu/)
or use Conda to create an R environment including latest R by:

``` bash
conda create --name r_env r-base
conda activate r_env # Activate env
conda update r-base # To update R
R # To open R
```

In order to install GEO packages (i.e. `sf`), you might need to install
GDAL on your system. Use the following to download GADL:

``` bash
sudo apt update
sudo apt install libudunits2-dev
sudo apt install libgdal-dev
sudo apt install gdal-bin
gdalinfo --version
```

Note that if you are a Conda user, you can use Conda to install your GEO
packages. Conda will install all dependencies.

We can also download **RStudio** from
[here](https://www.rstudio.com/products/rstudio/download/). To uninstall
RStudio, use:

``` bash
sudo apt remove rstudio
```

### Octave

We can install GNU Octave from the Ubuntu Software or use the following
command at a terminal prompt.

``` bash
sudo apt install octave
```

To open Octave run `octave` in a terminal prompt or click on GNU Octave
in the Application Overview. To use Octave in Jupyter Notebook, we need
to add Octave kernel to Jupyter Notebook. We can run the following
commands at a terminal prompt to add the kernel.

``` bash
conda config --add channels conda-forge
conda install octave_kernel
conda install texinfo # For using inline documentation (shift-tab)
```

### Julia

Download Julia Generic Linux Binaries for x86 from
[Julia](https://julialang.org/downloads/index.html) download page. Then,
extract the downloaded `.tar.gz` file to a folder on your computer (for
e.g. `/home`). To make things easier lets rename the extracted folder to
Julia. To run Julia, we can create a symbolic link (`ln -s`) from Julia
located in `/home/Julia/julia-1.1.0/bin/julia` to a folder that is on
the system PATH (for e.g. `/usr/local/bin/`). To do that run the
following command at a terminal prompt.

``` bash
sudo ln -s /home/Julia/julia-1.1.0/bin/julia /usr/local/bin/julia
```

To open Julia, run `julia` in a terminal prompt. To update, run the
following in Julia.

``` bash
using Pkg
Pkg.update()
```

We can add the Julia kernel to Jupyter Notebook by adding `IJulia` by
running the following in Julia.

``` bash
using Pkg
Pkg.add("IJulia")
```

You can use `exit()` command to exit from Julia. To uninstall Julia,
directly use:

``` bash
sudo apt remove julia
```

### Ruby

To install Ruby, run the following:

``` bash
sudo apt install ruby
```

`gem` is the package manger for Ruby. To update packages and remove old
versions use the following commands at a terminal prompt.

``` bash
sudo gem update --system # Update the RubyGems system software
sudo gem update
sudo gem cleanup
```

To install/uninstall packages use:

``` bash
sudo gem install pkg name
sudo gem uninstall pkg name
gem list # List of the installed packages
```

To use Ruby, run `irb` in a terminal prompt. We can use `exit()` command
to exit from Ruby. To write a long Ruby code, use a text editor and use
terminal prompt to run your code. For example, let assume we are going
to run `test.rb` in the Documents folder:

``` bash
ruby ~/Documents/test.rb
```

To uninstall Ruby, directly use:

``` bash
sudo apt remove ruby
```

### Gurobi

To install Gurobi Optimizer download the installer for 64-bit Linux from
[Gurobi download
center](http://www.gurobi.com/downloads/gurobi-optimizer). Gurobi
recommend `/opt` directory to install the software. To install the
`tar.gz` file in `/opt`, open the terminal and run the following
commands one by one (assume the `tar.gz` file is in the `Downloads/`):

``` bash
cd Downloads/
sudo mv gurobi8.1.0_linux64.tar.gz /opt
cd /opt/
sudo tar xvfz gurobi8.1.0_linux64.tar.gz
sudo rm gurobi8.1.0_linux64.tar.gz
```

We have to modify a few environment variables to allow Gurobi’s
executable files to be found when needed. Use `nano ~/.bashrc` to
open`.bashrc` file by nano text editor and add the following lines to
the file:

``` bash
export GUROBI_HOME="/opt/gurobi810/linux64"
export PATH="${PATH}:${GUROBI_HOME}/bin"
export LD_LIBRARY_PATH="${LD_LIBRARY_PATH}:${GUROBI_HOME}/lib"
```

Press `ctrl+o` to save changes and `ctrl+x` to exit from nano and then
close the terminal to set up the changes.

The next step is to install Gurobi license. To get an academic licence,
we need to register in Gurobi website and request for a free academic
licence. To obtain a Gurobi license key you will need to run the
`grbgetkey` command to retrieve your Gurobi license key. By default your
key will be stored in `/home/user` directory, we can move the key to
`/opt/gurobi/` if by:

``` bash
cd /opt/
mkdir gurobi
cd ~
sudo mv gurobi.lic /opt/gurobi
```

To get help, version information and the location of the current Gurobi
license file use:

``` bash
gurobi_cl --help
gurobi_cl --version
gurobi_cl --license
```

**For Python (Conda)**

From a terminal prompt issue the following commands to add the Gurobi
channel to your default search list and install the Gurobi package:

``` bash
conda config --add channels http://conda.anaconda.org/gurobi
conda install gurobi
```

We can remove the Gurobi package at any time by:

``` bash
conda remove gurobi
```

You may find more details
[here](http://www.gurobi.com/documentation/8.1/quickstart_windows/installing_the_anaconda_py.html#section:Anaconda).

**For R**

The R package file can be found in the `installerdir/R` directory of
your Gurobi installation. For a default installation of Gurobi 8.1.0,
use the following command in R:

``` bash
install.packages('/opt/gurobi810/linux64/R/gurobi_8.1-0_R_ver.tar.gz', repos=NULL)
```

We need to adjust the path to match your install directory and version.
You may find more details
[here](http://www.gurobi.com/documentation/8.1/quickstart_linux/r_installing_the_r_package.html).

**Examples**

There are several samples for R and Python in
`/opt/gurobi810/linux64/examples`.

---

Copyright, [Ashkan Mirzaee](https://ashki23.github.io/index.html) | Content is available under [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) | Sourcecode licensed under [GPL-3.0](https://www.gnu.org/licenses/gpl-3.0.en.html)
