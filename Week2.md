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

