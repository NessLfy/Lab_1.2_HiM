# Thursday 31/03/2022
##  Linux installation :
- Installation of manjaro

## Bash scripting tutorial [link](https://linuxconfig.org/bash-scripting-tutorial): 

## Git tutorial:

Git = version control system
It allows to keep track of versions of files. It allows for example to modify a document while keeping a "backup version". 

- Git commit graph: 

To initialise a repository : git init "repository name"

- 3 area in a git repo:

	- Working tree:
		- What we see in our file system (when we add delete file this is where it happens). Where we have possibility to edit everything
	- History:
		- Where the "log" of operation is , named .git. From there we can retrieve versions, see the changes who made them,... 
	- Staging Area (index):
		- Where the whole operation occurs, contains the last version of the commits. When you work on a file in the working system it then goes to the history through the staging area. 
		- Enables to have an intermediate between the changes on your computer and the git repository

- Basic commands: 
	- **git add**: to put changes from working tree to staging area
	- **git checkout -- filename** to retrieve a file from the staging area to the working tree
	- **git commit** to pass something to the history
	- **git reset HEAD** filename  to retrieve a version of a file from the history to the staging area
	- **git status** to see the current states of all the files
	- **git diff** to see the difference between working and staging
	- **git rm** remove file
	- **.gitignorefile** to create a file containing the names of the files/directory you don't whant a track of (usually logs, checkpoints of the code,... )

## Google cloud:
- Starting of a virtual machine
- installation of conda

# Friday 1/04/2022 
## Google cloud:
- Installation of pyHiM
	- Issue with the available size of the disk in the virtual machine. Only 10Go is available.
	- command to see the available space: 
```Bash
df -h 
```
- command to see which file is taking the most space
```bash
ncdu #Might have to install it 
```

To solve this issue you ca  just add more disk space when creating the virtual machine.  

## Github training
Creation of a github [repository](https://github.com/NessLfy/Lab_1.2_HiM) for the lab1 material

Branch the github to a computer in ssh:
- Create a ssh key in the computer by running :
```shell
ssh-keygen -t ed25519 -C nessim.louafi@protonmail.com   

```
this links an ID (ed25519) to an email adress (used for the github). Possibility to create a password at this step
- Add this identity to the machine:
```shell
ssh-add ~/.ssh/id_ed25519 
```
- Visualize the key (public hence the .pub) :
```shell
cat /home/nessim/.ssh/id_ed25519.pub
```

Enter this key in the github to have the access to the ssh.

Clone the github in a local repository:
- Create a repository folder in local
- clone the githb using the ssh key 
```shell
git clone git@github.com:NessLfy/Lab_1.2_HiM.git  
```

Now we can use the git commands to push , pull modify documents in the github.

Creation a branch to work on: 
```shell
git branch -M name of branch
```

