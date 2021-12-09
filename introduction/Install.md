Installing your own computing environment for PPDxP (<mark>Advanced</mark>)
===================================================

This page provides information for setting up a comparible computing environment on your personal computer.  **This is entirely optional and even actively discouraged, except for those who are already very confident in managing their systems.**

<font color=red>*These proceedures are provided for information only.  Neither the instructor nor teaching assistant will provide personal assistance with supporting your machine.  However, you are welcome to post questions and solutions in the class discsussion group and may find very helpful assistance from your peers.<br><br>
A fully functional working environment will be maintained on Rivanna for use in this class as described in the course web pages.  This is the only computing environment what will be supported by the staff.*
</font>

Linux System
----

The following instructions can reasonably be expected to work on any modern linux system to give you a compatible working environment to the one on Rivanna.

1) Download latest miniconda
miniconda provides a version of python (we'll use python3) along with the tools needed to create, install, and manage your own customized environments.
```
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh<br>
chmod +x Miniconda3-latest-Linux-x86_64.sh<br>
./Miniconda3-latest-Linux-x86_64.sh
```

Follow the instructions printed by the script and it's OK to accept the default choices.
(Btw graphical installers are also available..humbug!)

Executing the script creates a directory miniconda3 by default in your home area and modifies your .bashrc file to include the conda tools in your path. You can delete the miniconda script when you are finished.

(On MacOS use instead: https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-x86_64.sh)


2) For changes above to take effect, close and re-open your current shell, logout and back in or source ~/.bashrc again

A personal preference: If you'd prefer that conda's base environment not be activated on startup, set the auto_activate_base parameter to false.

```conda config --set auto_activate_base false```

3) Make sure the conda installer is up to data

```conda update -n base -c defaults conda```

4) Add the conda-forge repository

```
conda config --add channels conda-forge<br>
conda config --show channels<br>
conda config --set channel_priority strict<br>
```

The last command above gives conda-forge priority for ensuring that all packages are installed compatibly. This essentially forces compatibility with the most recent package versions in conda-forge.

5) Create an environment

```conda create -n PPDwP```

6) List your environments and actiate PPDwP
```
conda env list
conda activate PPDwP
```
# to deactivate the environment use
```
conda deactivate
```
Note: you will have to activate PPDwP each time you log in or open a new shell to start working. Therefore you may want to add the line activate PPDwP to the end of your .bashrc file.

7) Install the packages for PPDwP ( this step will take several minutes with a fast internet connection )

Make sure that your PPDwP environment is active before you enter the following commands

* install some common python packages
```conda install --yes scipy matplotlib seaborn sympy```

* install a jit python compiler and the ROOT analysis framework<br> n.b. installing ROOT also brings in a compatible C++ compiler and libs
```conda install --yes numba root jupyterlab```


* Looking over your environment

With the environment set up, your prompt should like something like
`(PPDwP) [rjh2j ~]$`
Within this environment your paths will be defined to access the programs and libraries you installed above. Try the following commands to see that you are not using your installed packahes and are not relying on the Rivanna's defaults:
```
printenv | grep miniconda3
which python
which g++
```

To see everything you just installed, type `conda list`

8) Install git

Finally, make sure *git* is installed.
We will use *git* throughout the semester to distribute examples and to facilitate teamwork on the exercises.

Type `which git` on your command line. If the *git* command is not found, you can install either by:

  * Using the packaging tools for your OS distrinution. For example, see this guide
  * Just add it to your conda environment using conda install git





MacOS System
----

For modern MasOS systems, simply follow the Linux System instructions above.  **Note: we have only verified this for computers with Intel processors.  If you have a new ARM-based Mac, we have no information on its compatibility with the tool installation.**

Windows System
-----
For Windows, we recommend that you use the Windows Linus Subsystem.   Details on Windows version compatibility and installation instructions can be found here: https://docs.microsoft.com/en-us/windows/wsl/install-win10

Installation steps for WSL:
* Follow the Manual Installation Steps given in the documentation
* When you need to choose a Linux distribuion, select Ubuntu 20.04 LTS
* Install an Xwindows server for Windows
  * Download and install Xming and Xming fonts unter the PublicDomeain release here: www.straightrunning.com/XmingNotes/
  * Note: Make sure to run Xlaunch before each WLS session.  You can choose the multiple windows option from the startup screen.

After your Linux subsystem session is running, follow the miniconda installation steps given in the Linux System instructions above.

Using a virtual machine
----

For Mac or Windows it is also possible to install a Linux distribution in a Virtual Machine and that installion can be configured using the steps above.
