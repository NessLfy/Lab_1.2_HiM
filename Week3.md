# Thursday 14/04/2022
Stardist

### Generate ground truth images
The goal is to work on poorly segmented images to segmente them "by hand" to retrain network. 

### Install labkit , QuPath and illastik
labkit was a fiji package to download directly from the fiji software

QuPath can be downloaded from the official [website](https://qupath.github.io/)

Illastik [aswell](https://www.ilastik.org/index.html)

## Getting the different images
The images are recorded by channel depending on the labeling: 

- Ch 00 : corresponds to the mask channel. A label that is specific to a region of the chromosome where specific genes will be labeled. Theoretically there are 2 regions per nuclei (for drosophila -> 2 loci)
- Ch 01 : corresponds to the barcode channel. Here and per round a different probe will be injected and label speciically a region of the mask
- Ch xx: DAPI used for localization of the nucleus

The images can be found here:

```shell
jupyter@krakatoa:/home/jupyter/tronador/data
```

We will work on different images for different channels corresponding to the different steps of labeling (different rounds). Note that for each round of labelling there is the mask channels that is the same (labelled at the first round). It is used to correct for drift and "localize" the different barcode to a specific region of the cell for further caracterization. 

Our first idea was to try to replicate results obtained in py-HiM and looking at the ability of the network to segment. 

Network used : 

```shell 
jupyter@krakatoa:/home/jupyter/tronador/pyHiM_AI_models/networks/

#network first used 

#'PSF_2D_stardist_18032021_single_loci','PSF_3D_stardist_20210618_simu_deconvolved_thresh_0_01'

```

Note that we used a 3D and a 2D network on a 3D image. When running the 3D network on one image we weren't able to replicate the image we were given as example: 

```shell
jupyter@krakatoa:/home/jupyter/tronador/data/scan_001_DAPI_004_ROI_converted_decon_ch00_segmentedMasks.png

#tested image

jupyter@krakatoa:/home/jupyter/tronador/data/scan_001_DAPI_004_ROI_converted_decon_ch00.tif
```

We then tried to apply a 2D network and see wether the image.png wasn't obtained like that. We then realized that the parameters of the 2D network would work for a 3D analysis. That is because we realized that the labelled "2D" network stardist_18032021_single_loci was in fact a 3D network. 

We then ran the labelled 2D network like a 3D network on the same test image to see wether we obtained the same result as the other 3D network. Our observation was that both 3D networks didn't yielded the same image.:
- The original 3D network yielded an image with a lot of labels that ressembled like small PSF (dots) which is what was expected . 
- The other network (2D_stardist_18032021_single_loci) yielded bigger objects, less round. 

Thus to compare the network further we decided to run an analysis on all the images in the folder recorded in channel 00.:
- We will manually compare the results by comparing all the label with the raw data. 
- Moreover we will compare both network for speed using the time package of python :

```python
#before the operation 
import time
start = time.time()

#after the operation

end = time.time() - start

```

Results for 12 images analyzed: 

"Real 3D" : PSF_3D_stardist_20210618_simu_deconvolved_thresh_0_01  = 30.1 min
"Not real 2D" : 2D_stardist_18032021_single_loci = 31.1minutes

Both network seemed to have a similar computing time. 

**Side project : Compare 3D and 2D for speed**
We we interested to se wether running a 3D analysis was really slower than 2D:
- What could be done would be to run a 2D analysis plane per plane on the 3D image and then stich the result in one image rather than running one 3D analysis (more complex and longer).
	- For that we need to test (using the time package) and also look at the stitching part of the algorithm to reconstruct a 3D segmented image. 
- One other we could look at would be the cellpose 3D algorithm that does this operation (2D analysis and 3D reconstruction). The difference is that cellpose does the analysis in all planes and in all direction of projection (z->z , x ->z , y-> z) and then reforms an image starting fromm all those analysis (might be really long)

# Friday 15/04/2022 
To save the images + the labels we used the package PIL (pillow) and ran:

Images are all ch00 i.e : mask channel

```python
from PIL import Image
import time 

cmap= random_label_cmap()

s = time.time()
for i in range(len(img)):
    moy = np.mean(img[i],axis=0)
    lbl_moy = np.max(lab[i],axis=0)
    plt.imshow(moy)
    plt.savefig('raw_project'+str(i)+' .png') #save the raw image
    plt.imshow(lbl_moy,cmap=cmap, origin="lower",alpha=0.4)
    plt.savefig('analysis'+ str(i)+'.png') #save the labelled image

end = time.time()-s 

print(str(end) +' s')
```

With img being a list of images (list of arrays) and lab a list of the labels found by stardist (list of array). Basically you create 2 images from arrays and then stich them together and save the resulting. Note that the img images are already normalized. All operations : 

```python 
cmap= random_label_cmap()


from PIL import Image

s = time.time()
for i in range(len(img)):
    moy = np.mean(img[i],axis=0)
    lbl_moy = np.max(lab[i],axis=0)
    plt.imshow(moy)
    plt.imshow(lbl_moy,cmap=cmap, origin="lower",alpha=0.4)
    plt.savefig('analysis'+ str(i)+'.png')

end = time.time()-s 

print(str(end) +' s')
```

## Metrics of segmentation
Our goal now is to try an find measures for the segmentation. Using the scikit.measure package we can retrieve information about each labels:

The first try is to look at one image  for all the planes (we could do for all the planes by making a z projection)

```python 
for i in range(len(labels)):
    
    test =labels[i]
    regions = regionprops(test,im[i])


    props = regionprops_table(test, intensity_image=im[i],properties=['centroid','eccentricity','equivalent_diameter_area','area','intensity_mean'])
    df = pd.DataFrame(props)
    print(np.max(df['intensity_mean']))
    
    plt.hist(df['intensity_mean'].values)
plt.show()
```

The goal is to plot each label (that has a specific value) once and thus have its maximum value of intensity instead of :. ![[plot1.png]]
