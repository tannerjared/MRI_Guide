How to Process MRI Images:

1. [Beginner's Guide to Command-Line Interface](primer)
2. [Install Programs](Home)
3. Preprocessing T1 images
     * [Convert DICOM to NIfTI](dcm2nii)
     * [Align anterior commissure and posterior commisure](acpcdetect)
     * [Correct intensity nonuniformities (bias field)](N4BiasFieldCorrection)
     * [Brain Extraction and Tissue Segmentation](antscorticalthickness)
4. Hippocampus Segmentation
     * [Placing Landmarks](hpc_landmarks)

---------------------------------------

Table of Contents:

[TOC]

---------------------------------------

Factors like patient position in the scanner, the scanner itself, and a host of unknown issues can result in brightness difference across the MR image. In other words, the intensity value (from black to white) can vary within the same tissue. This is known as a bias field. It's a low frequency smooth undesirable signal that corrupts MR images. The bias field results in inhomogeneities in the magnetic field of the MRI machine. The bias field if not corrected will cause all imaging processing algorithms like segmentation (e.g., Freesurfer) and classification to output incorrect results. A preprocessing step is needed to correct for the effect of bias field before doing segmentation or classification. 

![](http://www.slicer.org/slicerWiki/images/thumb/7/77/MRI_Bias_Field_Correction_Slicer3_close_up.png/560px-MRI_Bias_Field_Correction_Slicer3_close_up.png)

# Before you begin

You will need to set the environmental variables when you want to use the program:

```
#!console
$ export ANTSPATH=/usr/local/antsbin/bin/
$ PATH=${ANTSPATH}:${PATH}
```

# Using N4BiasFieldCorrection for the first time

To run the program, you should be able to type in a new Terminal window to see the available options:

```
#!console
$ N4BiasFieldCorrection --help

COMMAND: 
     N4BiasFieldCorrection
          N4 is a variant of the popular N3 (nonparameteric nonuniform normalization) 
          retrospective bias correction algorithm. Based on the assumption that the 
          corruption of the low frequency bias field can be modeled as a convolution of 
          the intensity histogram by a Gaussian, the basic algorithmic protocol is to 
          iterate between deconvolving the intensity histogram by a Gaussian, remapping 
          the intensities, and then spatially smoothing this result by a B-spline modeling 
          of the bias field itself. The modifications from and improvements obtained over 
          the original N3 algorithm are described in the following paper: N. Tustison et 
          al., N4ITK: Improved N3 Bias Correction, IEEE Transactions on Medical Imaging, 
          29(6):1310-1320, June 2010. 

OPTIONS: 
     -d, --image-dimensionality 2/3/4
          This option forces the image to be treated as a specified-dimensional image. If 
          not specified, N4 tries to infer the dimensionality from the input image. 

     -i, --input-image inputImageFilename
          A scalar image is expected as input for bias correction. Since N4 log transforms 
          the intensities, negative values or values close to zero should be processed 
          prior to correction. 

     -x, --mask-image maskImageFilename
          If a mask image is specified, the final bias correction is only performed in the 
          mask region. If a weight image is not specified, only intensity values inside 
          the masked region are used during the execution of the algorithm. If a weight 
          image is specified, only the non-zero weights are used in the execution of the 
          algorithm although the mask region defines where bias correction is performed in 
          the final output. Otherwise bias correction occurs over the entire image domain. 
          See also the option description for the weight image. 

     -w, --weight-image weightImageFilename
          The weight image allows the user to perform a relative weighting of specific 
          voxels during the B-spline fitting. For example, some studies have shown that N3 
          performed on white matter segmentations improves performance. If one has a 
          spatial probability map of the white matter, one can use this map to weight the 
          b-spline fitting towards those voxels which are more probabilistically 
          classified as white matter. See also the option description for the mask image. 

     -s, --shrink-factor 1/2/3/4/...
          Running N4 on large images can be time consuming. To lessen computation time, 
          the input image can be resampled. The shrink factor, specified as a single 
          integer, describes this resampling. Shrink factors <= 4 are commonly used. 

     -c, --convergence [<numberOfIterations=50x50x50x50>,<convergenceThreshold=0.0>]
          Convergence is determined by calculating the coefficient of variation between 
          subsequent iterations. When this value is less than the specified threshold from 
          the previous iteration or the maximum number of iterations is exceeded the 
          program terminates. Multiple resolutions can be specified by using 'x' between 
          the number of iterations at each resolution, e.g. 100x50x50. 

     -b, --bspline-fitting [splineDistance,<splineOrder=3>]
                           [initialMeshResolution,<splineOrder=3>]
          These options describe the b-spline fitting parameters. The initial b-spline 
          mesh at the coarsest resolution is specified either as the number of elements in 
          each dimension, e.g. 2x2x3 for 3-D images, or it can be specified as a single 
          scalar parameter which describes the isotropic sizing of the mesh elements. The 
          latter option is typically preferred. For each subsequent level, the spline 
          distance decreases in half, or equivalently, the number of mesh elements doubles 
          Cubic splines (order = 3) are typically used. 

     -t, --histogram-sharpening [<FWHM=0.15>,<wienerNoise=0.01>,<numberOfHistogramBins=200>]
          These options describe the histogram sharpening parameters, i.e. the 
          deconvolution step parameters described in the original N3 algorithm. The 
          default values have been shown to work fairly well. 

     -o, --output correctedImage
                  [correctedImage,<biasField>]
          The output consists of the bias corrected version of the input image. 
          Optionally, one can also output the estimated bias field. 

     -h 
          Print the help menu (short version). 

     --help 
          Print the help menu. 
          <VALUES>: 1
```

# Bias field correction

Correcting the bias field can be time consuming on the computer. One way to mitigate the computer processing time is to run the program several times on the same image from starting very coarse and moving in more finely:

```
#!console
$ N4BiasFieldCorrection -d 3 -i ~/<subjDir>/acpc.nii -o ~/<subjDir>/n4.nii.gz -s 8 -b [200] -c [50x50x50x50,0.000001]
$ N4BiasFieldCorrection -d 3 -i ~/<subjDir>/n4.nii.gz -o ~/<subjDir>/n4.nii.gz -s 4 -b [200] -c [50x50x50x50,0.000001]
$ N4BiasFieldCorrection -d 3 -i ~/<subjDir>/n4.nii.gz -o ~/<subjDir>/n4.nii.gz -s 2 -b [200] -c [50x50x50x50,0.000001]
```

### Note

This is the first step in the pipeline where I move from using just NIfTI files to zipped NIfTI (.nii.gz) files. Moving forward, some pipelines do not always accept NIfTI format and demand zipped NIfTI (.nii.gz). Although this isn't always going to be the case, using zipped NIfTI format has been the solution.