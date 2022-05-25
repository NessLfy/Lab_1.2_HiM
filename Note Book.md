 <h1 align="center">Day1 : _Thursday 31/03/2022_</h1> 
	

## Install linux 
- Download ISO into USB key  
- Install **manjaro**  
- Post installation :  
`nano /etc/hosts  `  
`192.168.8.10	krakatoa`  
`nano /etc/fstab`  
`192.168.8.60:/data/tronador /mnt/tronador nfs defaults 0 0`
`mkdir /mnt/tronador`  
`chmod 777 -R /mnt/tronador`  


##First step with Linux & bash  
- Linux terminal BASH scripting. [See tutorial](https://ubuntu.com/tutorials/command-line-for-beginners#1-overview)
- [BASH scripting](https://linuxconfig.org/bash-scripting-tutorial).
- [More comprehensive Linux tutorials](https://www.debian.org/doc/manuals/debian-reference/ch01.en.html)
- Advanced functions: 
 - [awk](https://www.geeksforgeeks.org/awk-command-unixlinux-examples/) (manipulating data and generating reports), 
 - [sed](https://www.gnu.org/software/sed/manual/sed.html) (stream editor : filter and modify text),   
 ` sed -i  's/Ali/Nessim/' qbio.txt` &rarr; change string
 - [find](https://danielmiessler.com/study/find/) (searches for files and directories in a directory hierarchy based on a user given expression),   
 - [xargs](https://shapeshed.com/unix-xargs/) (building and executing command lines from standard input).

<span style="color:red"> *add more details*</span>


## Introduction to Git  
	
- 	**install Git on manjaro**  
`sudo pacman -Syu` check if the system is up to date  
`sudo pacman -S git` Install Git  

- **Initializes a new Git repository**   
`git init` to place a project under revision control 

- **Configure Git username and email**  
`git config --global user.name "Ali kanso"` `git config --global user.email "kanso.ali@outlook.fr"`configure Git username and email to track when and who made changes in the commit  
`git config --list ` to check if the configurations were made  

###Basic Git commands
- `git status`  
Displays the state of the working directory and the staged snapshot
 
- `git add`   
Moves changes from the **working directory** to the **staging area**. This gives us the opportunity to prepare a snapshot before committing it to the official history.  
 `git add .` the "." add all new and modified files to the staging area 

- `git commit -m "choose message"`  
Takes the staged snapshot and commits it to the project history. Combined with `git add`, this defines the basic workflow Git users.  
 " -m " provide a short message describing what have been changed.  
If we check `git status` again, we will see a message saying "nothing to commit"

- `git log`    
Lets you explore the previous revisions of a project. It provides several formatting options for displaying committed snapshots. 

- `git diff`  
 shows difference between working tree and staging area. 
 For example if we git add a file and then modify it, it will display the changes between the new version and the snapshot. note that we can't see files that have not been "git added"     
`git diff --staged` diff of staging area and latest commit   


- `git rm `  
remove a file from the working tree and the staging area. we can check `git status` and we see that "deletes ..." has not been commited. &rarr; `git commit`

-  `git checkout -- <filename>`   
retrieve a file from the staging area into the working tree. git checkout is also the means to navigate existing branches  

- `git reset HEAD <filename>`  
 retrieve a file from the latest commit into the staging area.  
 then we can use `git checkout -- filename` to get it in the working tree.
 
- `git log -- <filename>`  
shows us the commits that includes filename. From here we can get the commit hash of the commit we want.    
`git checkout (commit hash) <filename>` will retrieve a file from a previous commit. this will put it in the working tree and the staging area. we can create a new commit for "restore s2"

- `<filename> .gitignore `  
if there is files or repos we don't want to track :
we create a file `ignore .gitignore` and we put everything we don't want there  
then we can `git add .` and commit 



## Exercises 3,4,6,9,10 from [here](https://www.redhat.com/sysadmin/linux-skills-home-lab)

### Exercise 3 


- difference `su` & `sudo` :  
`su` or super user, forces you to share your root password to other users whereas `sudo` makes it possible to execute system commands without root password. [reference 1]( https://www.tecmint.com/su-vs-sudo-and-how-to-configure-sudo-in-linux/ )  

- “ To grant access to sudo, the system administrator must edit the /etc/sudoers file. It is recommended that this file is edited using the visudo command instead of opening it directly with a text editor. ” [reference 2](https://www.tecmint.com/manage-users-and-groups-in-linux/)

`sudo visudo`

The next lines are used to specify permissions:  
  
**root        ALL=(ALL) ALL**  
The first ALL keyword indicates that this rule applies to all hosts.  
The second ALL indicates that the user in the first column can run commands with the privileges of any user.  
The third ALL means any command can be run.

**tecmint     ALL=/bin/yum update**  
If no user is specified after the = sign, sudo assumes the root user. In this case, user tecmint will be able to run yum update as root.

**gacanepa    ALL=NOPASSWD:/bin/updatedb**  
The NOPASSWD directive allows user gacanepa to run /bin/updatedb without needing to enter his password.

**%admin      ALL=(ALL) ALL**  
The % sign indicates that this line applies to a group called “admin”. The meaning of the rest of the line is identical to that of an regular user. This means that members of the group “admin” can run all commands as any user on all hosts.
  
### Exercise 4  
### Exercise 6
### Exercise 9
### Exercise 10
  


 <h1 align="center">Day2 : _Friday 01/04/2022_</h1> 

## Google cloud 

- Create a GC account and set up a virtual machine following these [tutorials](https://medium.com/google-cloud/set-up-anaconda-under-google-cloud-vm-on-windows-f71fc1064bd7)
- Install anaconda and [pyHiM] (https://github.com/marcnol/pyHiM) following these [tutorials](https://pyhim.readthedocs.io/en/latest/user_guide/pyhim_installation.html).  

**Conda** is a package and environment management tool that allows you to install Python packages on your computer as well as create and manage multiple Python environments, each containing different packages.

In order to create a conda environment, you first need to install an conda distribution. (**Anaconda** in our case)

Once conda is installed on the machine, we can create our conda environment:
We used a .yml file that can found in the development branch of pyHiM's github repository.  
So we had to `git checkout development` before `conda env create -f environment.yml`  
This will install all of the packages that we will need.

Do not forget to execute the Bash after you modify it.

There was not enough space on the VM (only 10Gb) so we had to create another VM and added more disk space(30Gb) and we also added more computig power 

Setting up the conda environment requires a .yml file that is found in the github repository of pyHiM in the development branch.

The afternoon we had a meeting on git command and made a github where we will put notebooks 

## Github repository

Go on [github](https://github.com) and create a new repository. [Lab_1.2_HiM](git@github.com:NessLfy/Lab_1.2_HiM.git)  

Branch the github to a computer in ssh:  

- Create a ssh key in the computer by running :
` ssh-keygen -t rsa -b 4096 -C "kanso.ali@outlook.fr" `

- add to the machine
`ssh-add ~/.ssh/id_rsa `

- Visualize the key 
`cat ~/.ssh/id_rsa.pub `

- Put the key on github to access to the ssh.

- clone the githb in a local repository using the ssh key 
`git clone git@github.com:NessLfy/Lab_1.2_HiM.git ` 

- Creation a branch and commit  
`git branch -m <name>`  
`git push origin HEAD`

- get access to all branches in this repository and you easily toggle between each to see each version and its files.  
`git branch -a`    

>   
 
  <h1 align="center">Day3 : _Thursday 07/04/2022_</h1> 
 
##  pyHiM test

Now that everything is set to run PyHiM :

- Get data from [Zenodo](https://zenodo.org/record/6351755)  
`pip install zenodo-get`  
`zenodo_get DOI of the data`

Run a test as described [here] (https://pyhim.readthedocs.io/en/latest/user_guide/pyhim_installation.html)

we can run pyHiM in the pyHiM repository by putting infoList.json in the folder containing the images

"A JSON file is a file that stores simple data structures and objects in JavaScript Object Notation (JSON) format, which is a standard data interchange format. It is primarily used for transmitting data between a web application and a server. JSON files are lightweight, text-based, human-readable, and can be edited using a text editor." [.JSON](https://fileinfo.com/extension/json)

piHyM will take his parameters from a .json file.

### Stardist & Cellpose
- [stardist](https://doi.org/10.1109/WACV45572.2020.9093435) 
- [cellpose](https://doi.org/10.1101/2020.02.02.931238)

<span style="color:red"> *add details about each one*</span>


 <h1 align="center">Day4 : _Friday 08/04/2022_</h1> 


##  Access a remote server 

ping (check command)

We started the day by learnig how to use `ssh` to access the server where the Data and Notebooks for segmentation are stored

ssh : Secure Shell, allows us to connect securely to a remote computer or a server by using a text-based interface.

We used **Local port forwarding (-L)**,this allows us to forward a connection from the client host to the SSH server host and then to the destination host port.

`ssh -L 8888:localhost:8888 jupyter@krakatoa`

`ssh -L <local_port>:<destination_host>:<destination_port> username@hostname`

We have been told not to use `-X` argument, this will log us into the remote machine, with X11 forwarding. Meaning, the executable file itself is hosted on a different machine than where the graphical interface is being displayed. The graphical windows are forwarded to the local machine through the SSH connection.

To lunch jupyter lab/notebook: 

in a different terminal window:  
`ssh jupyter@krakatoa`  
`conda activate jupyter`  
`jupyter notebook --no-browser --port 8889`


## Segmentation 

Get familiar with the scripts for stardist and cellpose segmentation.

<span style="color:red"> *explain both*</span>


### Create new conda environment
Cellpose needs some packages that are not compatible with stardist's packages. For that we created a new environment (cellpose_lab1) by cloning jupyter environment so we do not have to install everything from the scratch. 

`conda create --name cellpose_lab1 --clone jupyter`

Use `conda env list` to get a list of all environments

	
 <h1 align="center">Day5 : _Thursday 14/04/2022_</h1> 


## Stardist

Today we wanted to look at segmented images and try to segment undetected object manually

### Install labkit , QuPath and illastik
These are useful packages for segmentation and image analysis.  
labkit was downloaded directly from the fiji  
[QuPath](https://qupath.github.io/)  
[Illastik](https://www.ilastik.org/index.html)

### Images
We have been given a set of data that can be found in `jupyter@krakatoa:/home/jupyter/tronador/data`  

In the data set we can find images from 3 channel (ch00, ch01, chxx) each one correspond to different labeling  
- Ch 00 :  mask channel, labels specific genes in a region of the chromosome.  
- Ch 01 : corresponds to the barcode channel.   
- Ch xx: DAPI staining   

We first focused on **ch00**. The idea was to test two networks that have been trained previously and see if the segmentation is accurate.  
### Segmentation

The networks can be found in `jupyter@krakatoa:/home/jupyter/tronador/pyHiM_AI_models/networks/`

`'PSF_2D_stardist_18032021_single_loci'`, for me, it's a labeling error, the network is 3D

`'PSF_3D_stardist_20210618_simu_deconvolved_thresh_0_01'`for Nessim

We ran a segmentation on 12images with these two networks and compared the outputs.  They took more or less the same time (around 30min) 
 
Nessim's network showed small segmented objests with a round homogeneous shape while the other hand the output of my network was surprising. The segmented objects were big and had non uniform outline and have tendency to cluster, like if the same object was segmented multiple times. 

We saved the labeles and the normalized raw images in npy and tiff format

 <h1 align="center">Day6 : _Friday 15/04/2022_</h1> 


## Segmentation metrics 

Today's goal was to to find metrics for the segmentation and judge the capacity of the network when dealing with new data. 

We used scikit.measure package to obtain information about each label. it creates a table with the measures collected for each label.  We also did the same thing with raw images to retreeive measures based on the intensity.

<span style="color:red"> *to be completed*</span>

 <h1 align="center">Day7 : _Thursday 21/04/2022_</h1> 

## Performance of networks

Today we used scikit image directely on 3D images loaded as matrices 

The idea is to compare the two networks and see if they can detect the same thing.

We first conducted a qualitative analysis

#### Plotting a gallery of images
We got the centroids from all the labels and then report those coordinates in the raw image and croped 5 pixel aroud the location. We also used the centroid in z to center the plane for all objects and avoid working with projections. We then computed the intensity profile of all the cropped images and rank the images by intensity to have a measure of the range of detection.


 <h1 align="center">Day8 : _Friday 22/04/2022_</h1> 

### Metrics script

For the two networks, we plotted the intensity profile and intensity vs volume to see if we detected the same objects with a constant volume or not. We also showed detected object at low and high itensity for each network.

As we already noticed qualitatively, the plots showed that my network detected higher number and bigger objects compared to Nessim's network. We also saw a cut-off at 250 intensity, meaning that my network was not able to detect low intensity objects.

### Gallery collage and ranking by intensity

The code creates a collage of all the detected objects found by the network transposed to the raw image and ranked by increasing intensity 
We saw that the objects have no defined shape and and they all show high intensity


 <h1 align="center">Day9 : _Thursday 05/05/2022_</h1> 

## Compare Stardist and Starfind

We wanted to compare detections in Stardist and Starfind to correct the missing objects in stardist and retrain the network.
On my network, we first used starfind to detect objects on a raw image and then retreive the coordinates. We compared those coordinates to those in the labeled image to see if what was detected by starfind is also detected by stardist

Stardist works by detecting objects based on intensity thresholding. We can only change the **fwhm** and **threshold** of intensity

We started by splitting the big image to smaller images (256x256). This step is done to make the computation faster and it's preferable for later to train with small images. For that I used a fonction called `view_as_blocks` from scikit-image.

Then we varied the parameters of starfind and calculated the accuracy by dividing the number of object detected in stardist over the number of object detected in starfind *100

The analysis was done on this image : scan_002_RT17_004_ROI_converted_decon_ch00 and showed over 80% accuracy
with FWHM= 3 and th = 9 (we made a code to estimate the best parameters) 



 <h1 align="center">Day10 : _Friday 06/05/2022_</h1> 

In the morning we worked on cleaning our code and create fonctions to make it easy to execute  
## Automatize corrections

The next step is to find a way to automatize the correction on the raw image (add spots on the image where the network did not detect an object).   
The idea is to add a sphere using a spot that was well-detected by the network as a template.



 <h1 align="center">Day11 : _Monday 09/05/2022_</h1> 


As we saw before, we get the coordinates (x,y) of detected object in Starfind and verify if we have a label having the same coordinates in Stardist. For the correction it's the same idea. but we also need to know z to be able to place the sphere correctly. For that, with the (x,y) that we got, we will look at this position on the raw image and find the z plane with the highest intesity.

I noticed when I checked the accuracy on the full image and the splitted image, it was higher on the full image. this is due to the fact that we have more edges with splitted images and the objects near the edges can not be dtected and corrected.  
so I will do my corrections on the big image and splitted it afterwards.



 <h1 align="center">Day12 : _Tuesday 10/05/2022_</h1> 

## New training dataset :

We will perform correction only on images that showed a significant number of undetected objects 

To start, The full images were corrected and we obtained labeled images. Then, we removed a plane over 2 to make the training easier and faster. The images were then relabeled to ensure that the labeling worked. As we said before, we splitted the images (raw and labeled) to smaller images (256x256). Finally, we check for corrections and save the raw and the corrected croped images (80% for training and 20% for testing).



