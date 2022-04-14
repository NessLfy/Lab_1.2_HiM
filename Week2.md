# Thursday 07/04/2022
## Set up another virtual machine and pyHiM test
Set up of a virtual machine on google cloud with more disc space and more computing power to install pyHiM and test it.

- [tutorial](https://medium.com/google-cloud/set-up-anaconda-under-google-cloud-vm-on-windows-f71fc1064bd7) to create a virtual machine. 
- install conda 
- follow installation instruction of pyHiM [here](https://pyhim.readthedocs.io/en/latest/user_guide/pyhim_installation.html).
- to get a sample data use the zenodo platform [Zenodo](https://zenodo.org/record/6351755)

To extract the data from Zenodo platform we installled zenodo_get on the virtual machine from the [zenodo_website](https://zenodo.org/record/1261813#.Yk6UH7mxXJE) then running:
```python
pip install zenodo-get

 ```

Then to use zenodo_get just run:

```shell 
zenodo_get DOI of the data
```

Followed the installation trial of pyHiM and running pyHiM

Problem with conda environment: 

A conda envrionment is a place where you can create version of packages, python,.. different from the base (like a git branch) to avoid conflict between programs. 
Setting up the conda environment requires a .yml file that is found in the github repository of pyHiM in the development branch. 

```shell 
git checkout development

conda env create -f environment.yml

```

**!! When changing the bashrc during the installation (to change the pythonpath) always remember to relaunch the terminal either by physically relauche it or by simply running bash in the terminal**

After that a pyHiM environment is created with all the required packages needed to run pyHiM.

To run it: 
- Download images
- 2 options:
	- Either copy the infoList.json file in the folder containing the images and run pyHiM in the pyHiM repository folder
	- Copy the configuration files to the directory where you want to run pyHiM:
	```shell
	cp /home/rata/Repositories/pyHiM/modelParameterFiles_JSON/infoList*json path-to-your-directory
	```
	to run pyHiM: 
	```shell 
	pyHiM.py -F .
	```

piHyM works by taking parameters from a .json file to use for its different module. In the case of AI segmentation, it needs the path where AI algorithm are found. However pyHiM can be executed module by module because each modules writes its output in the disk. 

To have all the modules: 
```shell 
pyHiM --help

pyHiM -C module1,module2,module3

```

Outputs are folders containing all the outputs of the operations (png and npy files for display and further operations respectivly) and files containings summarry of what has been done ( .log and .md)

## Xargs tutorial
Xargs is a command that allow to combine operations. It takes as arguments the output of the previous command like: 


```shell
echo 'one two three' | xargs mkdir

#outputs 

#3 folders one two and three

```

Can be combined with a % to perform severall operations : 

```shell
> cat foo.txt
one
two
three

> cat foo.txt | xargs -I % sh -c 'echo %; mkdir %'
one 
two
three

> ls 
one two three
```

## Awk tutorial 
from [this website](https://www.geeksforgeeks.org/awk-command-unixlinux-examples/)
Awk is a command programming language that allows to perform operation without having to script it. 

**WHAT CAN WE DO WITH AWK?** 

**AWK Operations:**   
(a) Scans a file line by line   
(b) Splits each input line into fields   
(c) Compares input line/fields to pattern   
(d) Performs action(s) on matched lines 

**General synthax**

```shell 
awk options 'selection _criteria {action }' input-file > output-file
```

## Sed tutorial
from [this website](https://www.gnu.org/software/sed/manual/sed.html)
Sed is a stram editor used to perform basic text transformations. 

**Example of synthax** 

This will replace all occurrences of ‘hello’ to ‘world’ in the file input.txt

```shell 
sed 's/hello/world/' input.txt > output.txt
```

### Stardist & Cellpose
[stardist](https://doi.org/10.1109/WACV45572.2020.9093435) , [cellpose](https://doi.org/10.1101/2020.02.02.931238)
<<<<<<< HEAD
=======

# Friday 08/04/2022 
## Initiation to segmentation scripts
The scripts/data are stored on a server. To access them we need to connect to it via ssh. Ssh is a program for logging into a remote machine and for executing commands on a remote machine. Ssh connects and logs into the specified destination, which may be specified as either [user@]hostname or a URI of the form ssh://[user@]hostname[:port].

The simplest command: 

The synthax is : ssh -*arg* *disk@nameofmachine*

```shell
ssh -X jupyter@krakatoa     
```

The argument -X allows permission to the user and enables to send commands and retrieve graphic outputs. We can run jupyter notebook/lab with this type of connection but the outputs will be very slow as the informations needs to be sent received computed and resent to the local machine. 

To solve this issue, we can map a specific port in the remote compute to a port in the local machine via ssh so that the information can be sent in the local machine computed by the remote and displayed directly in the local machine. 

```shell 
ssh -L 8888:localhost:8888 jupyter@krakatoa
```

Here we specify:
- the port we want to bind in the remote machine 
- the port in the local machine 
- the name of the remote machine

To lunch jupyter lab/notebook: 

We can create another connection (normal) to avoid crowding the terminal that created the link by running in another window :

```shell
ssh jupyter@krakatoa
```

then activating the conda environment:

```shell
conda activate jupyter
```

Now we can lunch jupyter notebook/lab in the remote machine by specifying that there is no need for a browser (because the connection will be sent to a specific port) and specifying the port to send to. 

```shell
jupyter notebook --no-browser --port 8888
```

### Creation of a conda environment
To run the cellpose pipeline required certain packages that were not available in the jupyter environment. To be able to use it without destabilizing the jupyter environment we created a neww environment (cellpose_lab1) based on the jupyter environment by running in the base environment of krakatoa:

```shell
conda create --name cellpose_lab1 --clone jupyter
```

To verify that the environment was created run : 

```shell 
conda env list
#or
conda info --envs 
```

Then we installed the packages required for cellpose by running: 

```shell
pip install *packagename*
```

>>>>>>> 00bbda7 (week3 day 1)
