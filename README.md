 " Dear Nessim and Ali  

We are also looking forward to your course.
We put together with JB a few tutorials and guides to get the basics. If you want to start looking into them, it will considerably speed up the first couple of weeks of learning before you get your hands dirty,
if you have any question, do not hesitate to ask us  
best  

marcelo "


## Lab1 subject

Hi-M is a novel imaging technology developed in the lab that permits imaging of tens to hundreds of genomic loci and RNA species at once. This method generates large amounts of data (>2 Tb) per experiment that need to be processed by custom-made image analysis pipelines based on Artificial Intelligence methods. Use of super-computer centers and cloud computing resources has become critical for these analyses.

## Technical tools to be used:

Linux, console scripting, parallel computing, artificial intelligence, high-performace computing

## Objectives:

Become acquainted with Linux, bash scripting, AI-based image analysis, develop and benchmark image analysis pipelines using high-performace clusters and cloud computing.


## Detailed program :

### I- Installation of a working environment using Linux and online tools:

#### I-a- First step with Linux & bash:

- Linux terminal BASH scripting. [See tutorial](https://ubuntu.com/tutorials/command-line-for-beginners#1-overview)
- [BASH scripting](https://linuxconfig.org/bash-scripting-tutorial).
- [More comprehensive Linux tutorials](https://www.debian.org/doc/manuals/debian-reference/ch01.en.html)
- Advanced functions: [awk](https://www.geeksforgeeks.org/awk-command-unixlinux-examples/), [sed](https://www.gnu.org/software/sed/manual/sed.html), [find](https://danielmiessler.com/study/find/).

#### I-b- Quick introduction to git :

- Introduction video can be found [here](https://www.youtube.com/watch?v=uR6G2v_WsRA)

#### I-c- Setting up a Google colab account :

Colab is an online tool allowing for developing jupyter notebooks (for example for AI)

- create a google colab account (gmail adress)
- google colab [tutorial](https://colab.research.google.com/notebooks/intro.ipynb)
- exercises:
  - Deploy pipeline for running AI image segmentation, and AI training in google collab.

#### I-d- Google Cloud

- create account GC
- follow this [tutorials](https://medium.com/google-cloud/set-up-anaconda-under-google-cloud-vm-on-windows-f71fc1064bd7)
- exercises:
  - start virtual machine
  - install conda
  - install [pyHiM](https://github.com/marcnol/pyHiM). Installation instructions [here](https://pyhim.readthedocs.io/en/latest/user_guide/pyhim_installation.html).
  - get data from [Zenodo](https://zenodo.org/record/6351755). Hint: install `zenodo_get`.
  - test pyHiM run

#### I-e- Set-up your own Linux computer and install manjaro

- download ISO into USB key
- install
- follow post-installation configuration instructions.
- Do exercises 3,4,6,9,10 from [here](https://www.redhat.com/sysadmin/linux-skills-home-lab)

`Marcelo TODO`: Locate images that work and that do not work. Move to tronador.

### II- AI & Deep Learning :

- Learn how to apply AI pipelines to segment images: stardist, starpose.
- Learn how to train an AI network using already available training set.
- Build your own training sets using imageJ or cellpose tools or Ilastik. Use them to generate new networks for:
  - mouse
  - fly brain
- Test networks and validate them

#### AI tutorials

- 4 **short** introductive videos created by Anna Kreshuk on Machine Learning and Deep Learning :

	video 1 : [https://www.youtube.com/watch?v=-TDNDv2C6ow](https://www.youtube.com/watch?v=-TDNDv2C6ow)

	video 2 : [https://www.youtube.com/watch?v=-RmipXviG8E](https://www.youtube.com/watch?v=-RmipXviG8E)

	video 3 : [https://www.youtube.com/watch?v=_dNc7odIRiM](https://www.youtube.com/watch?v=_dNc7odIRiM)

	video 4 : [https://www.youtube.com/watch?v=-hHtfd9JrAg](https://www.youtube.com/watch?v=-hHtfd9JrAg)

- two you tube channels for Machine Learning & Deep Learning :
- [Code Basics](https://www.youtube.com/playlist?list=PLeo1K3hjS3uu7CxAacxVndI4bE_o3BDtO)
- [Fidle CNRS](https://www.youtube.com/c/CNRSFormationFIDLE?app=desktop)
- a seminar video on Stardist - the first 20minutes are very didactic :
[https://www.youtube.com/watch?v=Amn_eHRGX5M](https://www.youtube.com/watch?v=Amn_eHRGX5M)
- Finally, three reviews that are well written and quite extensive on DL and applications.
  - [Moen et al. Nature Methods. 2019](https://drive.google.com/file/d/1_Z_0Qevg-usSxsmZ2uEjQ14jCce-7wpq/view?usp=sharing)
  - [Von Chamier et al. Biochem. Soc. Trans. 2021](https://drive.google.com/file/d/1rYyhp6CrV8IOpQP96-FqIpNWtn3d5jZf/view?usp=sharing)
  - [Greener et al. Nature Mol. Cell. Biol. 2021](https://drive.google.com/file/d/1qjDKzOPliiP0VAnGVZLu7nrwb8W1wsJX/view?usp=sharing)
  
