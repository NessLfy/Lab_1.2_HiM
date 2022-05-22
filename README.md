# Lab notebook repositories for our Lab1.2 project HiM


Welcome to our repositories. You will find 2 branches corresponding to our respective lab notebooks. 


In this branch you will find my lab notebook separated per week with details. In this file is a general summary of everything that was done.

# Week 1: Introduction to linux

In this first week the goal was to get familiar with linux and the command line. Moreover get introduced to the concept of virtual machine, the git language and first glance at the pyHiM package.

# Week 2: Initiation to segmentation scripts

The goal for this week was to have a first experience with pyHiM by running it on a virtual machine on sample images and with the different segmentation scripts. The segmentation scripts were the 3D stardist and 2D cellpose

# Week 3: Network(s) testing

Testing of 3D/ 2D segmentation on new images for the networks. Comparison of 2 different segmentation networks in 3D (speed/accuracy). Begining of plotting segmentation result to evaluate accuracy of the segmentation :

- plotting the intensity per segmented object to see wether there could be different population which could correspond to a bad segmentation.

Outlooks to pursue:

- speed of 3D network compared to 2D network for all planes

- testing of cellpose 3D segmentation via 2D network

- further characterization of the results of segmentation

- finding other metrics.


# Week 4 : Qualitative and quantitative metrics development

Further investigation of evaluation metrics and development of a standardized analysis pipeline for segementation result quantification and network performance comparisson. 
Qualitative evaluation by transposing segmented object coordinate to the raw image. Begining of quantification of intensity range of segmentation by comparing the result of segmentation of an intensity threshold technique (starfind) and the AI network. This final step will give further infromation about the network perfomance, it is able to detect with high precisionhigh intensity objects or lower precision but also lower intensity objects ? 

Outlooks: 

- Finalize pipeline of quantification of stardist vs starfind

- Compare the 2 networks with this metric

- Use the starfind image to generate a ground truth from the labeled image from stardist and retrain the networks. 

*Notebooks: krakatoa_run_stardist_exploring results.ipynb, krakatoa_run_stardist_exploring metrics.ipynb* 

# Week 5: Comparing stardist and starfind
The goal was to evaluate the performance of a network to detect high intensity objects. To do so we compared the algorithm Starfind with the output of the network.

We tested different things first: 
- The accuracy of the network : the number of objects detected by both astropy and stardist / number f object detected by astropy
- The stability of the accuracy when varying the FWHM parameter of astropy
- The stability of the accuracy when varying the threshold of detection (sigma abvoe background) 

We concluded that the network acheived between 75 and 85 % accuracy when the parameters of astropy where FWHM = 3 and threshold = 9 x the mean intensity of the image

*Notebook : Updating_stardist_with_astropy_exploratory.ipynb*

# Week 6 : Updating starfind with stardist 
With the observation made the previous week, the goal was to develop a pipeline that would update stardist based on astropy. The idea is to correct the labeled image from stardist with objects detected by astropy missed by the network. Thus , generating new ground truth images for network retraining. 

*Notebook : Updating_stardist_with_astropy_final_pipeline.ipynb*

# Week 7 : Training and testing results of training

With the newly generated dataset we ran a couple of trainings using the same parameters as the training of the first network used. We then explored the results using the metrics we developped. 

## Useful tips

To make the text aligned everywhere we created a css file containg the code below :

```css
.cm-s-obsidian, .markdown-preview-view {
  text-align: justify;
  hyphens: auto;
}
```

**Note : the file needs to be in the folded *.obsidian/snippets* of the vault** 
