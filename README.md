# Introduction

Original source repo : https://github.com/Biscactus/vscode_latex_config

This installation guide will help you set up a LaTeX environment in Visual Studio Code within a WSL2 (Windows Subsystem for Linux) environment. It also covers the integration with GitHub for versioning and collaboration.

# Table of Contents
- [Introduction](#introduction)
- [Table of Contents](#table-of-contents)
- [Install Ubuntu 20.04 in WSL2](#install-ubuntu-2004-in-wsl2)
  - [Verification and Configuration](#verification-and-configuration)
- [Setup GitHub](#setup-github)
  - [In the Terminal](#in-the-terminal)
  - [In GitHub](#in-github)
  - [Clone this Repository (or Any Repository)](#clone-this-repository-or-any-repository)
- [Install Visual Studio Code](#install-visual-studio-code)
- [Use LaTeX in Visual Studio Code through Ubuntu](#use-latex-in-visual-studio-code-through-ubuntu)
- [Install Python in Ubuntu](#install-python-in-ubuntu)
- [Use GitHub for Collaboration](#use-github-for-collaboration)

# Install Ubuntu 20.04 in WSL2

Open Windows PowerShell terminal as an administrator and execute the following command:

```bash
wsl --install -d Ubuntu-20.04
```

This command will download the WSL2 (Windows Subsystem for Linux) version of Ubuntu. It is important to download version 20.04 as other versions may not work. Once the download is complete, restart your PC.

## Verification and Configuration

To use Ubuntu, open the Windows terminal and click on the downward-facing arrow in the tab bar above the terminal window. From there, you can change your terminal preference. Choose "Ubuntu" to use Ubuntu as your terminal. To set the Ubuntu terminal as the default when you open your terminal instead of Windows PowerShell, click on "Settings." Under "Startup," click on "Default profile" and choose Ubuntu.

Once you have opened the Ubuntu terminal, you will be prompted to create a username and a password. The username will be displayed at the start of every line, and the password will be required for downloading files.

After choosing a username and password, execute the following two commands to ensure that the latest version of Ubuntu 20.04 is installed:

```bash
sudo apt update
```

```bash
sudo apt upgrade
```

You can verify the Ubuntu version at any point by executing the following command:

```bash
wslfetch
```

This command will display the Ubuntu logo in ASCII art on the left and your Ubuntu version on the right.

# Setup GitHub

To configure the link with GitHub, you must first create a GitHub account at https://github.com/.

## In the Terminal

In your Ubuntu terminal, execute the following commands, replacing "username" with your GitHub username:

```bash
git config --global user.name "Username"
```

Replace "example@gmail.com" with the email address you used to create your GitHub account:

```bash
git config --global user.email example@gmail.com
```

To obtain an SSH key to provide to GitHub, execute the following command:

```bash
ssh-keygen
```

Leave all the values empty or at their default settings by pressing Enter at each step (directory, passphrase, passphrase validation).

Next, copy the **public** SSH key by executing the following command and copying the displayed text:

```bash
cat ~/.ssh/id_rsa.pub
```

The public key should look something like this:

```
AAAAB3NzaC1yc2EAAAADAQABAAABAQC3RiOdvxC/+qW0IDpb0UGPFgFOMqKLzzJ MxRLNbRN2QIcC

vLbLUI0UmzOYvLoawXtmv3W3N+kvVCKc/ED+hAOorx1P2ZaFbyzim6PjBU 0tBGKWZoN5DsMfy4xo7h1IO5uugFjC7KyDLfCUk+1gAuiDDYy2hLZn+Agfh9oG6YONVEYDX+OZeNK0UhwNahZxjwAa349VT4FmVWlSyVX0c2ZlwEUogXfKrM3IFjH+bqOwKCWL1BjNdi/geJ9tlRTiy4lpa5AWrdHCpz7NuBfXbaMjEjgH doc@hill-valley
```

## In GitHub

1. Open GitHub and log in to your account.
2. Click on your profile icon in the top-right corner and select "Settings."
3. In the left sidebar, click on "SSH and GPG keys."
4. Under "SSH Keys," click on "New SSH key."
5. Provide a name for the key and paste the **public** key you obtained from your Linux terminal.

Your GitHub account is now linked with your Linux terminal.

## Clone this Repository (or Any Repository)

Go back to your terminal and enter the following command:

```bash
cd
```

This command will bring you back to the "home" folder in your Linux workspace. The folders you access with "cd" are all within the "home" folder, as indicated by `(\\wsl.localhost\Ubuntu-20.04\home)`.

If you type `cd` alone, it will bring you back to the first folder in the chain, which is the home folder. You can learn more about Linux commands at https://ubuntu.com/tutorials/command-line-for-beginners.

To clone a GitHub repository, navigate to the repository on your favorite internet browser. Click on the "Code" button, which will open a small pop-up menu. From this menu, select "SSH" and copy the SSH key.

Back in your terminal, type the following command, replacing "SSHkey" with the key you copied:

```bash
git clone SSHkey
```

After executing this command, if you run `ls`, you should see the name of the repository you just cloned.

# Install Visual Studio Code

Visit https://code.visualstudio.com/ and download Visual Studio Code as you would any other software.

Now, in your Ubuntu terminal, use the `cd` command to navigate to the directory of the repository you cloned. If you cloned this repository in your home folder, the command would be:

```bash
cd latex-config-master
```

Next, execute the following command:

```bash
code .
```

To ensure seamless integration with WSL2, go to the extensions page in VSCode and download the WSL extension (local).

Additionally, download the following extensions on your WSL2 installation:
1. Jupyter
2. LTex - LanguageTool
3. LaTex Workshop
4. Python
5. Pylance
6. Rainbow CSV (pour + de clarté dans les CSV)
7. Material Icon Theme (pour une meilleure visualisation du type de fichier)
8. CSV to LaTeX Table Generator
9. Edit CSV

# Use LaTeX in Visual Studio Code through Ubuntu

Open your Ubuntu terminal and execute the following commands:

```bash
sudo apt update
```

```bash
sudo apt install texlive-full
```

These commands will install LaTeX on your Linux subsystem. The installation process may take some time, but you don't need to do anything during this time.

Once

 the installation is complete, execute the following commands:

```bash
sudo apt update
```

```bash
sudo apt upgrade
```

To write LaTeX, it is essential to have the .json file from this repository. You can now use LaTeX in Visual Studio Code through your WSL2 Ubuntu installation. Only one small step remains!

# Install Python in Ubuntu

To install Python in Ubuntu, use the following command:

```bash
sudo apt install python3
```
For usage with VS Code, you need to specify which Python version should be called by default. To do this, enter the following command:
```bash
sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 1
```
You now have a default Python version that you can verify using:
```bash
python -V
```
If the Python version is displayed, you can now use PythonTeX by following the example in main.tex. Make sure that your settings.json is the same as the one in this repository for it to work correctly.

It might also be necessary to install Pygments for PythonTeX to function:
```bash
pip install Pygments
```
If pip is not installed:
```bash
sudo apt install python3-pip
```
Then repeat the command to install Pygments.

To make graphs in Python, matplotlib and pandas are very useful.
To install matplotlib, execute the command:
```c
python -m pip install -U matplotlib
```
To install pandas:
```c
pip install pandas
```

# Use GitHub for Collaboration
Now, when you create a new repository in your WSL2 system, go to your repository and execute the command: 
```bash
git init
```
This will initialize a git environnement inside your workspace. Now if you want to collaborate, you need to create your own branch and be sure that you always work in your branch and never in the master. To create your branche, execute the following command by replacing "branch-name" by your own branch name. 
```bash
git branch branch-name
```
Make all modifications, making sure they are in the branch and not in the master.
Once the changes in the branch have been committed and pushed, to merge the branch, execute the following command in the terminal: 
```bash
git pull origin master
```
Resolve conflicts in vscode.

Once the conflicts are resolved, go to GitHub and create a pull request. If the conflicts have been successfully resolved, the merge can be done automatically.