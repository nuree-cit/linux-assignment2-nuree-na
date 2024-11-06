# linux-assignment2-nuree-na

# Linux Assignment 2 Scripts Guide

--- 

## project-1
The project-1 directory contains 4 files:
3 scripts:
- **configRepo** = a script that clones given repository and creates symbolic links.
- **installPackage** = a script that installs packages from a file provided.
- **main** = a script that calls and controls other two scripts.
1 file:
- **packages** = a list of package names to install.
### To run the script 'main'
- Must be in the directory contains `configRepo`, `installPackage` and `main`.
- Must use `sudo` privilege. 
- Must provide at least one of the options:
	- `-i` to install packages:
		- an argument is required: `FILENAME`
		- `packages` file contains default packages.
		- user can add, modify and/or delete, this file `packages` or use another file.
	- `-c` to clone and config repository:
		- an argument is required: `USERNAME`
### Scripts details
#### `configRepo`
- This script does two main things:
- take a `user name`
- **1. gitClone**
	- cloning repository "https://gitlab.com/cit2420/2420-as2-starting-files.git" to the `user`'s home directory.
- **2. createSymbolicLink**
	- creating symbolic links:
		- from `home/user/bin` to `cloned_repository/bin`
		- from `home/user/.config` to `cloned_repository/config`
		- from `home/.bashrc` to `cloned_repository/home/bashrc`
#### `installPackage`
- This script does one main things:
- take a file that contains list of package names to install.
- **1. installPackages**
	- update current packages 
	- compare that given file to a list of currently installed packages.
		- if a package exists:
			- skip it
		- if a package does not exist:
			- install it
#### `main`
- This script does one main things:
- Calls two other scripts and run it with `getopts` option control.  
- **1. Initial checking for error handling.**
	- User must be in the direcotry with required scripts `configRepo`, `installPackage` and `main`.
	- User must run this script with `sudo` previllege. 
	- User must provide options.
	- User must follow the option syntax (starts with dash '-')
- **2. checking options and arguments**
	- `-i`: Installation
		- an argument `filename` is required.
		- `filename` = a file that contains package names to install.
		- check a file `packages` and give it as an argument.
	- `-c`: Cloning and Configuring
		- an argument `username` is required.
		- `username` = a user to clone and create symbolic links

---
## project-2
The project-2 directory contains 1 file:
1 script:
- **addUser** = a script that creates a new user.
### To run the script 'addUser'
- Must use `sudo` privilege. 
- Must provide both options:
	- `-u` to make a new user name:
		- an argument is required: `USERNAME`
		- `USERNAME` must be unique.
			- If not, try again.
	- `-s` specify a shell type to use:
		- an argument is required: `SHELLTYPE`
		- `SHELLTYPE` must be a full path of valid shell type.
			- eg. `/bin/bash`
- Optionally provide option:
	- `-g` to add user to other groups:
		- an argument is required: `GROUPNAME`
		- multiple arguments are accepted.
			- eg. `group1 group2 group3`
### Scripts details
#### `addUser`
- This script does one main things:
- create a new user
- **1. Initial checking for error handling.**
	- User must run this script with `sudo` previllege. 
	- User must provide options.
	- User must follow the option syntax (starts with dash '-')
- **2. checking options and arguments**
	- `-u`: user name
		- an option `-u` is required.
		- an argument `username` is required.
		- `username` = a user name to use.
		- `username` may be unavailable.
	- `-s`: shell type
		- an option `-s` is required.
		- an argument `shelltype` is required.
		- `shelltype` = a shell type to use.
		- `shelltype` may be invalid.	
	- `-g`: group name
		- an argument `groupname` is required.
		- multiple arguments are accepted.
		- `groupname` = a group name to add.
		- `groupname` may not exists.
- **3. creating user account**
	- check and assign available user id and group id.
	- check if user name is available and if the shell type is valid.
	- create a new user by adding line to `/etc/passwd` file.
	- add to a default group by adding line to `/etc/group` file.
	- make a home directory for the new user.
	- change ownership of a new home directory to the new user.
	- copy files from directory `/etc/skel/` to a new user's home directory.
	- if additional groups are given, add the new user in them.
	- print the new user's information
	- run `passwd` to create a password for a new user