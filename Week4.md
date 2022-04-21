# Thrusday 21/04/2022 
## Metrics and performance evaluation

raw= np.load('Outputs/raw/RT11_raw.npy')

print(raw.shape)

lab = np.load('Outputs/labeled/RT11_lab.npy')

print(lab.shape)

properties = ['label', 'area','intensity_max','intensity_mean','centroid_weighted']

region = regionprops_table(lab,intensity_image=raw,properties = properties)
df = pd.DataFrame(region)


Iterate for all files 
fig , ax = plt.subplots(1,2)
fig.set_size_inches(10,5)

s = time.time()

file_list_r = [x for x in glob('Outputs/raw/'+os.sep+"*.npy") if "00" in x and "ch00" in x]
file_list_l = [x for x in glob('Outputs/labeled/'+os.sep+"*.npy") if "00" in x and "ch00" in x]

counter = 0

for i,j in zip(file_list_r,file_list_l):
    intensity = []
    region = 0
    lab = np.load(j)
    im = np.load(i)
    region = regionprops(lab,im)
    for k in range(len(region)):
        intensity.append(region[k].intensity_max)
    print(np.mean(intensity))
    ax[0].hist(intensity,label = counter ,alpha= 0.4)
    ax[1].hist(intensity,label = counter ,alpha= 0.4)
    ax[1].set_xlim(45000,70000)
    ax[1].set_ylim(0,20)
    counter += 1
    
end = time.time() - s 

print(str(end/60)+ ' min')

    
ax[0].set_xlabel('Intensity')
ax[1].set_xlabel('Intensity')
ax[0].set_ylabel('Count')
ax[1].set_ylabel('Count')
plt.legend()
plt.show()

compare 2 different networks

fig , ax = plt.subplots(1,2)
fig.set_size_inches(10,5)

s = time.time()

file_list_l = [x for x in glob('../Ali/segmentations/npy_labels/'+os.sep+"*.npy") if "00" in x and "ch00" in x]
file_list_r = [x for x in glob('../Ali/segmentations/npy_images/'+os.sep+"*.npy") if "00" in x and "ch00" in x]

counter = 0

for i,j in zip(file_list_r,file_list_l):
    intensity = []
    region = 0
    lab = np.load(j)
    im = np.load(i)
    region = regionprops(lab,im)
    for k in range(len(region)):
        intensity.append(region[k].intensity_max)
    print(np.mean(intensity))
    ax[0].hist(intensity,label = counter ,alpha= 0.4)
    ax[1].hist(intensity,label = counter ,alpha= 0.4)
    ax[1].set_xlim(45000,70000)
    ax[1].set_ylim(0,20)
    counter += 1

end = time.time() - s 

print(str(end/60)+ ' min')

ax[0].set_xlabel('Intensity')
ax[1].set_xlabel('Intensity')
ax[0].set_ylabel('Count')
ax[1].set_ylabel('Count')
plt.legend()
plt.show()



Ideas to move forward:

-   Start from the raw image and run starfind to detect the objects and get coordinates. See if those coordinates are also present in the labeled image (would be a measure of how many true points are detected by the network)
-   Start from the labeled image and frome those coordinate in the raw image crop the raw image and display a montage of all the segmented points to see wether the network detectyed something real or not. We could also classify them by increasing intensity to make it more pretty

Stardist :

mean, median, std = sigma_clipped_stats(data, sigma=3.0)  
print((mean, median, std))  

daofind = DAOStarFinder(fwhm=3.0, threshold=5.*std)  
sources = daofind(data)  
for col in sources.colnames:  
    sources[col].info.format = '%.8g'  # for consistent table output
print(sources)  

crop the projection 

properties = ['label', 'area','centroid']

df = pd.DataFrame(regionprops_table(lab_moy,intensity_image=data,properties = properties))

pos = []
for i in df.index:
    pos.append(list(df.iloc[i, 2:]))

crop = []
for j in range(len(pos)):
    crop.append(data[round(pos[j][0]-5):round(pos[j][0]+5),round(pos[j][1]-5):round(pos[j][1]+5)])

plot everything 

_, axs = plt.subplots(10, 13, figsize=(30, 30))
axs = axs.flatten()
for img, ax in zip(crop, axs):
    ax.imshow(img)
plt.show()


crop in 3D 

properties = ['label', 'area','centroid']

df_2 = pd.DataFrame(regionprops_table(lab,intensity_image=raw,properties = properties))

pos_2 = []
for i in df_2.index:
    pos_2.append(list(df_2.iloc[i, 2:]))

crop_2 = []

for j in range(len(pos_2)):
    crop_2.append(raw[round(pos_2[j][0]),round(pos_2[j][1]-5):round(pos_2[j][1]+5),round(pos_2[j][2]-5):round(pos_2[j][2]+5)])
