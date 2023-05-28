# Inter-IIT-ISRO-2023

### Google Drive Link to work on: [Link](https://drive.google.com/drive/folders/11FiTwiMUyVE1lkbSG6gU9WpdbcG7EVpS?usp=share_link)

DATASET LINK:

OHRC datas downloaded:[Link](https://drive.google.com/drive/folders/1nU4i1s1Kwo2A5bcMNpRvAqTK6ikSogk0?usp=share_link)

TMC data downloaded : [Link](https://drive.google.com/drive/folders/1OEmK24mGoaSdu2dZx2hNBBBCgqNO00f9?usp=sharing)

### Cropped OHRC train-test datatset : [Link](https://www.kaggle.com/datasets/arijitdas2002/tudumm) 

As we know that the problem statement is regarding enchancement of low resolution images(TMC dataset) to higher resolution, we used **SRResnet model**.

The srresnet.ipynb file contains the code for the model of 21 layer deep network which we have used to train the images i.e from Low resolution to High Resolution images. We have trained the images and saved the weights of the model .

**Training Data**
OHRC images are cropped to 1024x1024 dimensions and saved as .png files to be used for training. These images are de-resolutioned during traning to create input and corresponding output.

#### <ins>Overlap_calculator.ipynb</ins>

This code will help you to find the common parts of OHRC and TMC2 images and then cut out the largest rectangle which could be used for our training where the TMC2 part will be our input variable to our model and OHRC part will be our target variable to our model

#### <ins>SRResNet_training.ipynb</ins>

Training pipeline for a 21 layer SRResNet using OHRC coropped data itself. We deresolution the image 8-times in the dataloader and train the model to preduce output 8 times up-resolutioned than the input. We compare the outputs with the original OHRC images and use L1 loss to perform backpropagation using ADAM optimizer. (128x128 dimentional crops are used as model input due to GPU resource constraints). Weights are saved and used for inference

#### <ins>read_TMC_and_stitch_(without_model).ipynb</ins>
TMC images are large but model inputs are of fixed size (128x128). So we crop 128x128 patches from a TMC image, pass them through the model and then stitch them again back in their corresponding places. This notebook explores that approach without the model predictions but using the crops in their place to stitch back.

#### <ins>SRResNet_inference_(approach_1).ipynb</ins>
This is as the approach as explained above, but this approach is a bit too costly on the RAM due to all the stitching happening. This approach may be adopted in availability of enough resources.

#### <ins>SRResNet_inference_(approach_2).ipynb</ins>
In liue with difficulty stated above, we explored another approach where we save every row as '.tif' file and store them. Later we stitch all the rows to build the complete image.

To exceute, run all cells of the ipynb files.

<ins>Note</ins> : 
Take care of the directory addresses, and change them accordingly if needed 

## Installation :

We used ***PDS4 Viewer*** software for viewing large xml files. Following is the installation code in python for the same:

``` !pip install pds4_tools```

After finding the overlapping patch in TMC and OHRC images, we need to get the rectangular image of maximum area, for that we used **MaxRect** library. Following is the installation code :

```https://pypi.org/project/maxrect/```

``` pip install git+https://${GITHUB_TOKEN}@github.com/planetlabs/maxrect.git```

We used the ***Spectral Angle Mapper*** as metric for validating our model. We imported that metric from **TorchMetrics**, the installation code is :

```
!pip install torchmetrics 
from torchmetrics import SpectralAngleMapper 
```

## Stacks Used :
- [pds4_tools](https://pypi.org/project/pds4-tools/)

- [skimage](https://scikit-image.org/)

- [torchmetrics](https://pypi.org/project/torchmetrics/)

- [glob](https://github.com/python/cpython/blob/3.11/Lib/glob.py)

- [tqdm](https://tqdm.github.io/)

- [PIL](https://pypi.org/project/Pillow/)

## Results :
![alt text](https://github.com/Arunim10/Inter-IIT-ISRO-2023-MID-PREP/blob/main/images/prediction.jpg)
