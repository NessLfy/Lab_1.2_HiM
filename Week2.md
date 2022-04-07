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
