# Inline 3D Cocnrete Printing (I3DCP) dataset

The present dataset was collected at the 3D printing laboratory of the École des Ponts ParisTech, in France. It features 628 images acquired during a 3D concrete printing session. If using this dataset, kindly cite the next article:

```
@article{monitoring_3d_concrete,
title = {Automatic monitoring of 3D concrete printing using computer vision},
year = {2022},
author = {Rodrigo Rill-García and Eva Dokladalova and Petr Dokládal and Romain Mesnil and Pierre Margerit},
keywords = {Automatic monitoring, 3D concrete printing, Image processing, Deep learning},
}
```

Detailed information about the image acquisition setup, illustrated below, is presented in the article.

An example of acquired image is shown below. The 628 raw images, contained in "raw_images" folder, are named img_XXX.tiff; XXX goes from 000 to 627.

![alt text](https://github.com/Sutadasuto/I3DCP/blob/main/readme_illustrations/img_000.png?raw=true)

Additionally to the raw images, we provide two sets of annotations. The first set corresponds to binary segmentation masks of interstitial lines, as illustrated below. These binary images are contained in the "interstitial_region_segmentations" folder; inside that folder, the files are divided into a "training" folder with 128 images and a "testing" folder with 32 images. Each file is named img_XXX.png, where img_XXX denotes the corresponding image in "raw_images"; the approximate width of the annotated lines in the png images is 20 pixels.

![alt text](https://github.com/Sutadasuto/I3DCP/blob/main/readme_illustrations/segmentation_example.png?raw=true)

The second set of annotations corresponds to texture classification of windows extracted from the raw images. The individual texture windows are contained in the "texture_windows" folder, containing 447 images; these files are named img_XXX-YYY.tiff, where img_XXX denotes the name of the original raw image and YYY denotes the window number within the img_XXX.tiff image in the "texture_images" folder. Before window extraction, the raw images are leveled to reduce the impact of shadows and lightning while preserving textural information (read the article for further details); inside the "texture_images" folder, we include the images after leveling (with the name img_XXX_leveled.tiff).

![alt text](https://github.com/Sutadasuto/I3DCP/blob/main/readme_illustrations/window_example.png?raw=true)

We provide labels for 111 windows, contained in the root of the dataset in the form of a csv file named "texture_windows-labels.csv". This dataset is composed by two columns: 1) "image", containing the file name of the texture window; 2) "class", a number between 0 and 3 corresponding to one of the four possible classes:

0. Fluid: characterized by a smooth surface. Since the fluidness is associated with high water content, this class is also characterized by a high reflectance
1. Good: it corresponds to the desired material properties. The amount of present water is reduced, producing the appearance of more visible grains on the surface with higher homogeneity and a lower reflectance
2. Dry: characterized by a rougher texture, caused by an increased amount of visible grains with bigger size. Since the amount of water is reduced, the material exhibits very low to no reflectance. However, this class is also determined by the absence of cracks
3. Tearing: characterized by the appearance of cracks. It is also identified by the lack of reflectance and often by a rougher texture than the dry class

![alt text](https://github.com/Sutadasuto/I3DCP/blob/main/readme_illustrations/textures_example.png?raw=true)

The labeling was performed by the agreement of two annotators following the next ruleset:
 * Any class other than "good" is considered a "defect"
 * A window right below the center of the printing nozzle must be ignored
 * If a window contains different simultaneous textures:
   * If a defect exists, provide the label of the defect if it occupies >30% of the surface
     * In presence of simultaneous defects, select the class with the major area
 * If the image is out of focus, it is ignored

From the 111 labeled images, the distribution of classes is: 24 fluid, 27 good, 24 dry and 36 tearing.

