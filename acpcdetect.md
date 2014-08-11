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

The acpcdetect program is a great program for aligning the anterior commissure and posterior commissure along the same horizontal line in sagittal view:

![](http://classconnection.s3.amazonaws.com/925/flashcards/1329925/png/2011-08-13_23271313318867635-1425D8484BE3E3AD7B8.png)

As well as making sure the brain isn't tilted in along the coronal plane or transverse plane. In other words, the interhemispheric fissure should be straight in the coronal and transverse view:

![](http://classconnection.s3.amazonaws.com/985/flashcards/1077985/jpg/81326744185093.jpg =300px)

# Before you begin

You will need to set the environmental variables when you want to use the program:

```
#!console
$ ARTHOME=/usr/local/art
$ export ARTHOME
```

# Using acpcdetect for the first time

To run the program, you should be able to type in a new Terminal window to see the available options:

```
#!console
$ acpcdetect --help
Usage: acpcdetect [-V/-version -h/-help -v/-verbose -m/-model <model> -rvsps <r> -rac <r> -rpc <r>]
[-O/-orient <code> -D -M] [-o/-output <output volume> -oo <output orientation code>]
[-onx <int> -ony <int> -onz <int> -odx <float> -ody <float> -odz <float> -sform -qform -noppm -notxt]
[-AC <int> <int> <int>] [-T <filename>]
-i/-image <input volume>

Required arguments:
-i or -image <input volume>: Input (test) image volume in NIFTI format of type `short'

Optional arguments:
-h or -help: Prints help information.
-v or -verbose : Enables verbose mode
-m or -model <model>: User-specified template model (default = $ARTHOME/T1acpc.mdl)
-rvsps <r>: Search radius for VSPS (default = 50 mm)
-rac <r>: Search radius for AC (default = 15 mm)
-rpc <r>: Search radius for PC (default = 15 mm)
-O or -orient <code>: Three-letter orientation code (See users' guide for more details). Examples:
		PIL for Posterior-Inferior-Left
		RAS for Right-Anterior-Superior
-o or -output <filename>: If this option is present, the program outputs an AC/PC and MSP aligned image
with the given filename.
-oo <output orientation code>: Three-letter orientation code of the output image.  If this is not
specified, then the output image will have the same orientation as the input image.
-onx, -ony, -onz: x/y/z matrix dimensions of the output image (default=same as input image).
-odx, -ody, -odz: x/y/z voxel dimensions of the output image (default=same as input image).
-M: Make the midpoint between AC and PC the center of the output FOV.
-T <filename>: Writes output rigid-body transformation matrix to specified <filename>.
-D: Prints additional information

Outputs:
<input volume>_ACPC_sagittal.ppm: Sagittal view of the detected AC/PC locations
<input volume>_ACPC_axial.ppm: Axial view of the detected AC/PC locations
<input volume>_ACPC.txt: Stores the detected AC/PC coordinates and the estimated mid-sagittal plane
```

# AC-PC aligning T1 image

This program works on T1 images in the NIfTI format. The simplest code to use is:

```
#!console
$ acpcdetect -M -o ~/<subjDir>/acpc.nii -i ~/<subjDir>/cot1.nii
```

**Why adjust the FOV center?**

When dealing with smaller brains or brains of various sizes, if you make the center of the field of view (FOV) at the anterior commissure, you often mistakenly remove part of the occipital lobe, because the anterior commissure is so far forward / anterior. Instead, you want to move the center of the FOV backwards and the easiest way to standardize that is to place the center of the FOV at the midway point between the anterior commissure and the posterior commissure.

### Note

The acpcdetect program will not be able to use zipped NIfTI files (e.g., .nii.gz), so all methods up to this point leave the files in NIfTI format and not zipped NIfTI format.
