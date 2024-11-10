# acit2420-assignment2 - Shell Scripting Assignment


# Introduction
Project 1 - System Setup Scripts: These scripts are used to setup a user's system. It involves installing pacakges from a user-defined list of packages and then creates symbolic links to configuration files.

Project 2 - User Creation Script: This script is used to automate and create a user. This includes setting a password, establishing preliminary group memberships, creating a home directory, and configuring the user's shell.

# Project 1 - System Setup Scripts

The main script `main_script` is used to interact with the other scripts in the project:
1. `package_installer`: This script installs kakoune and tmux packages defined in a `packages.txt`. Once the script reads through the list of packages, it will use `pacman` package manager to install the dependencies required. If the packages are already installed, it will skip it and move on to the next one.

2. `symlink_script`: This script clones the repository from https://gitlab.com/cit2420/2420-as2-starting-files.git using git clone and creates symbolic links for configuration files (in our case, kak, tmux, and bashrc) located within the user's home directory. If the symbolic link already exists, it will echo out an error.


The `main_script` is the script that the user interacts with which allows you to choose which action to perform by passing command-line options using getopts. It can run both the package installer and symlink configuration scripts, or just one of them.

# How to Use the Script

## Prerequisites

Firstly, make sure you have a stable internet connection before beginning this process.  
Next, check that you have git installed on your Arch Linux system by typing in your terminal: `git --version`.  
If not, type `sudo pacman -S git` into the terminal

Lastly, when running these scripts, make sure you are either the root user or have sudo privileges.

## Running the Scripts using main_script
 1. To run the main_script, type `sudo bash ./main_script`
 - Since there is no argument, it will print the help message as well as how to use and call the script.
 2. Script Options 
  - `-i` displays the help message and usage information  
  `sudo bash ./main_script -i`

 - `-p` runs the package installer script   
  `sudo bash ./main_script -p`

- `-s` runs the symbolic link script  
  `sudo bash ./main_script -p`

- `-x` runs both the package installer and symbolic link scripts  
  `sudo bash ./main_script -x`

## Notes
It is recommended to run these scripts by purely interacting with the main_script as it takes command-line options and outputs instructions.

## package_installer Script

First, this script checks if `packages.txt` exists and is in the right location, then it will begin to loop through the packages inside the file and call `pacman -Syu --noconfirm "$package"` to install each package. `--noconfirm` helps with not needing to enter a confirmation button for every package.

## symlink_script Script

First, this script checks who is running the script and what privilege they are running it with, then it creates the necessary directories before creating the symbolic links.  

This script will create symbolic links for:
### bin
`/home/USER/cloned_repo/bin/sayhi` to `/home/USER/bin/sayhi`  
`/home/USER/cloned_repo/bin/install-fonts` to `/home/USER/bin/install-fonts`

### config
`/home/USER/cloned_repo/config/kakrc` to `/home/USER/.config/kakrc`  
`/home/USER/cloned_repo/config/tmux/tmux.conf` to `/home/USER/.config/tmux/tmux.conf`

### bashrc
`/home/USER/cloned_repo/home/bashrc` to `/home/USER/.bashrc`

# Project 2 - User Creation Script

## DISCLAIMER
The script is unfinished.

## Introduction
The script `new_user_script` was supposed to take in command-line options to set a new user's information. It then runs the script and creates a new user. The script will try to find the next available user ID and group ID for the new user and group. After the home directory is created, the script would copy the `etc/skel` folder into the home directory. Lastly, it will prompt to change the user's password using `passwd $username`



