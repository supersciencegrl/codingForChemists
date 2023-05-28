# Creating a Python Environment

## Contents

- [Creating a Python Environment](#creating-a-python-environment)
  - [Contents](#contents)
  - [Introduction](#introduction)
  - [Why Python Environments?](#why-python-environments)
  - [Option 1: Installing Anaconda or Miniconda](#option-1-installing-anaconda-or-miniconda)
    - [Creating and Using a `conda` Environment](#creating-and-using-a-conda-environment)
    - [Installing Packages Into Your `conda` Environment](#installing-packages-into-your-conda-environment)
  - [Option 2: Installing Python from python.org](#option-2-installing-python-from-pythonorg)
    - [Creating and Using a `venv` Virtual Environment](#creating-and-using-a-venv-virtual-environment)
    - [Installing Packages Into Your `venv` Environment](#installing-packages-into-your-venv-environment)
  - [Other Options](#other-options)

## Introduction

The goal is to enable you to create a python "environment" 
for each of your projects, 
tailored to its requirements.

This guide will be opinionated. 
If you want to use another method than one described here, 
my advice would be to use that one method consistently. 
If you start using multiple methods, 
you run the risk of becoming XKCD \#1987:

![XKCD #1987](https://imgs.xkcd.com/comics/python_environment.png)

This guide is focused on macOS and Windows installations.
Linux can be trickier.
One warning for Linux users:
If you want to create virtual environments using `venv`, 
as described in this guide,
some Linux distributions don't include `venv` with python,
and you'll have to install it separately.

## Why Python Environments?

You may think, 
"my computer already has Python on it. Why can't I just use that?"
The problem is that this "system Python" is used by your operating system,
and if you try to customize it by installing Python packages 
something might break.
It's Python's extensibility
that makes it so powerful and so widely useful, 
so it is highly likely that you will want 
to install additional libraries at some point.

For example, if you want to do data analysis and visualization, 
you are very early on going to be installing libraries 
such as `pandas` and `matplotlib`.
If you are following a tutorial, 
and at some point it the instructions say something like:

```bash
pip install pandas
```

or

```bash
conda install pandas
```

you will want to make sure you are installing these 
into a Python environment of your own, separate from system Python.

At this point, if you started searching online
how to go about downloading Python 
and creating environments, 
you'd probably find many, conflicting, recommendations on how to do this. 
I will recommend two methods in this guide:

1. Installing Anaconda (or miniconda), 
   and managing virtual environments with `conda`.
   This is probably the best solution for people, 
   particularly those with scientific interests, to get started. 
   If you're interested in programming for data analysis and visualization, 
   you can also obtain R this way.
   An Anaconda installation also makes it easy to start using Jupyter Notebooks,
   which are a great way to start learning Python interactively. 
2. Installing Python directly from python.org,
   and creating virtual environments with `venv`.
   This is a minimalist approach.

## Option 1: Installing Anaconda or Miniconda

   A full Anaconda installs a lot of stuff on your computer 
   that you may not need. 
   However, if you're just starting out in programming,
   this is the easiest option.
   If hard drive space is a concern, you can install miniconda instead. 
   [This guide](https://docs.anaconda.com/free/anaconda/getting-started/distro-or-miniconda/) 
   on the Anaconda web site summarizes how to choose between the two.

   [Caltech's Be/Bi103 course](https://bebi103a.github.io/lessons/00/index.html) 
   (Introduction to Data Analysis in the Biological Sciences) 
   has great guides for setting up a python environment via Anaconda. 
   The key steps are summarized below.

   1. Download the 
      [Anaconda](https://www.anaconda.com/download/) 
      or [miniconda](https://docs.conda.io/en/latest/miniconda.html) 
      installer and run it.

      - choose "Install for Me Only" if you are given that option
      - you may be prompted to install a (free) JetBrains IDE 
        such as PyCharm or DataSpell. 
        Unless you know you want to use it, skip this—
        you can always install it later if you want.
   2. Open a command-line interface (CLI). 
      - On macOS or Linux,
      where a bash-like command line is standard,
      a command prompt ending in "`$`" 
      precedes the cursor where you start typing.
      Its exact text will be specific to your computer 
      and where you opened the CLI from.
      However, your prompt should include "`(base)`", 
      which indicates which conda environment you're currently using 
      (here, the default "base" environment). 
      For the terminal commands below, 
      "`(environmentname)$`" represents the command prompt 
      (and is not part of the commands you are entering in the CLI).
      - Windows users should use the "Anaconda Prompt" as the CLI. 
      This is similar to Windows' "command prompt" CLI, 
      but with redirections ("PATH") to conda libraries 
      automatically set up for you. 
      You can enter "anaconda prompt" into the Windows search bar 
      to find this application.
   3. Update your base conda installation and environment. 
      It is a good idea to run the following commands 
      not only after the initial installation, 
      but every few weeks-to-months[^1]. 

      [^1]: When the author returned to his office computer 
      after COVID remote working ended, 
      its `conda` was so far out of date 
      that `conda update conda` would no longer work. 
      The `conda` updater needed a newer version of python, which could not be updated using the old `conda` version—Catch 22.
      A complete uninstall and reinstall of Anaconda was required.

      ```bash
      (base)$ conda update conda
      ```
      Follow the prompts to update conda itself, and then:
      ```bash
      (base)$ conda update --all
      ```
      and follow the prompts to update all the installed libraries.

### Creating and Using a `conda` Environment

Although you can work from the base conda environment, 
for your own projects you will want to create an isolated environment.
You'll be able to install only what you need for that project,
and you can specify the versions of all the libraries to avoid conflicts.
It is very easy to create environments with conda, 
and switch between environments as needed.

A detailed guide can be found on the 
[Anaconda website](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html). 
To get started, here are the most useful commands:

- `conda create` is used to create a new environment.
  For example, 
  if you were taking the Be/Bi 103 course 
  and wanted to create an environment for it, 
  you could do the following:
  ```bash
  (base)$ conda create --name bebi103
  ```
  However, that course requires that Python 3.9 is used, 
  to make sure that all their code runs as originally written. 
  Most likely, when you downloaded conda, 
  you chose the most recent python for the base conda environment.
  If you know you need a specific python version, 
  include it when you create the environment:
  ```bash
  (base)$ conda create --name bebi103 python=3.9
  ```
  You can also add specific packages that you want via this command, but it's not necessary. Installing packages is covered in the next section.
- `conda env list` will list all your environments, e.g.:
  ```bash
  (base)$ conda env list
   # conda environments:
   #
   base                  *  /Users/myname/opt/anaconda3
   bebi103                  /Users/myname/opt/anaconda3/envs/bebi103
  ```
  The asterisk indicates the current active environment, which is still `base`.
  Note the location of your new environment inside the `/envs` folder.
  Every conda environment you create will be in a subfolder of `/envs`.
- `conda activate` is used to switch to another environment, e.g.:
  ```bash
  (base)$ conda activate bebi103
  (bebi103)$
  ```
- `conda list` will list all the packages installed in the active environment.

-  To deactivate the environment and return to using your base conda python:
   ```bash
   (bebi103)$ deactivate
   (base)
   ```
  - If you are already in your base conda environment, and you `deactivate`,
    you may exit conda completely.
    You'll no longer see an environment name in parentheses,
    and you'll be using whatever the non-conda default python is.
    If you didn't intend to do this,
    you can use `conda activate base` to go back.


### Installing Packages Into Your `conda` Environment

An important difference when using conda environments is that, 
as much as possible, 
packages should **not** be installed using a `pip install`-like command, 
which is normally how Python packages are installed. 
For the packages you want to install, 
search online for installation instructions 
and see if there is a conda option.

If there is, 
often `conda install {packagename}` works,
but sometimes a specific "channel" must be listed 
for conda to find the package.
For example, to install `pandas`, 
[follow the online instructions](https://anaconda.org/anaconda/pandas) 
to install it from the "anaconda" channel:
```bash
(bebi103)$ conda install -c anaconda pandas
```

Some packages do not have a conda installer. 
To "pip install" packages into your environment:

1. Make sure `pip` is installed in your current environment 
   (and not just the base environment), e.g. 
   ```bash
   (current_environment)$ conda install -n bebi103 pip
   ```
   This will install `pip` specifically to the bebi103 environment, 
   regardless of whatever `current_environment` may be active.
2. To install a python package into your current environment:
   ```
   python -m pip install name_of_package
   ```
   **Note the use of `python -m`.** 
   If you just `pip install` a package, 
   [it may not get installed where you intended](https://snarky.ca/why-you-should-use-python-m-pip/).

   You can always find out which python interpreter you're currently using 
   by entering `which python`(macOS/linux) or `where python`(Windows) 
   in the command line. 
   Then, `python -m pip install` will install packages to that environment.

## Option 2: Installing Python from python.org

[This guide](https://pythontest.com/python/installing-python-3-11/) from Brian Okken covers the basic installation:
1. Go to [python.org](https://www.python.org/).
2. Hover over "Downloads". If you want the most recent release of Python,
   a button for its download will appear in the popup window.
   If you want to install a different Python version,
   or additional Python versions,
   you can click on "view the full list of downloads",
   and download a specific version from their list.
3. Run the installer.
     - **Windows users**: Check out Okken's guide. 
       Specifically, don't click too quickly through the installer dialog. 
       When you reach “Advanced Features”,
       check the box for “Add Python to environment variables”.

### Creating and Using a `venv` Virtual Environment
A new user searching online can find many, conflicting ways 
to create a virtual environment. 
The current standard method is to 
[use the `venv` command](https://docs.python.org/3/library/venv.html). 
Ignore any guides that use the `virtualenv` command instead—
these are out of date.

Whereas conda environments can be used across projects,
it is most common to include venv environments 
either in the top level of your project folder, 
or one folder above it. 
The former seems to be more common. 
So, if your project's code is contained in the directory `my_awesome_project`:

1. Open a terminal with `my_awesome_project` as the current working directory.
   For example, on macOS/linux using a bash terminal
   you can switch to that directory using `cd`, 
   then double-check that you are in the right place using `pwd`:
   ```bash
   $ cd ~/my/path/to/my_awesome_project
   $ pwd
   /Users/myname/my/path/to/my_awesome_project
   ```
2. From the command line, enter:
   ```bash
   python -m venv .venv
   ```
   This creates a folder named .venv within my_awesome_project 
   that contains your virtual environment. 
   This would use your default python version. 
   If you want to use another installed python version for a project, 
   you can specify it like:
   ```bash
   python3.9 -m venv .venv
   ```
   > Naming the environment `.venv` or `.env` is a common convention,
   > but you can use whatever name you want.
   > Note that file names that begin with "." 
   > are often hidden from you by default.
   > It's a way of denoting files 
   > that you usually don't want to modify directly,
   > e.g. critical system files are often named this way 
   > to protect them from accidental corruption by users.
   > To see hidden folders using your OS's file browser,
   > see [this guide](https://www.sonarworks.com/support/sonarworks/360003040160-Troubleshooting/360003204140-Troubleshooting/5005750481554-How-to-show-hidden-files-Mac-and-Windows-).
   > To include hidden files when using `ls` from a bash command line,
   > use `ls -a`.

3. Activate the virtual environment: 
   assuming a virtual environment folder named `.venv` 
   (as in the previous step):
   macOS:
   ```bash
   $ source .venv/bin/activate
   ```

   Windows cmd.exe command line:
   ```cmd
   $ .venv\Scripts\activate.bat
   ```

   Windows Powershell:
   ```powershell
   $ .venv\Scripts\Activate.ps1
   ```

   Note: if PowerShell gives an error message saying running scripts is disabled,
   enter the following command in PowerShell[^2]:

   [^2]: See [the python venv documentation]() for details.

   ```powershell
   $ Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
   ```
   To deactivate the environment and return to using your system python:
   ```bash
   deactivate
   ```

### Installing Packages Into Your `venv` Environment

To "pip install" packages into your environment:

1. Activate the environment as described in the previous section.
2. Check that you are using the python inside your virtual environment, 
   using `which python`(macOS) or `where python`(Windows).
3. To install a python package into your current environment:
   ```
   python -m pip install name_of_package
   ```
   **Note the use of `python -m`.** 
   If you just `pip install` a package, 
   [it may not get installed where you intended](https://snarky.ca/why-you-should-use-python-m-pip/).

## Other Options

- On macOS, homebrew can be used to install Python. 
  However, the author thinks that combining homebrew python installation 
  with other methods such as (Ana)conda can lead to XKCD #1987.
- Power users, especially those writing python packages, 
  can look at pyenv or asdf. 
  The author strongly recommends 
  [*Publishing Python Packages*](https://www.manning.com/books/publishing-python-packages)
  by Dane Hillard to see an example 
  of a publishing toolset that includes asdf.
