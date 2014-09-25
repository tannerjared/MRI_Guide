How to Process MRI Images:

1. [Beginner's Guide to Command-Line Interface](begin_primer)
2. [How to Install Programs](Home)
	 * [Specific instructions for installing programs on Fulton Supercomputing Lab](https://bitbucket.org/njhunsaker/fsl)
3. Preprocessing T1 images
     * [Download example files](https://bitbucket.org/njhunsaker/preprocessing-t1-example)
     * [Convert DICOM to NIfTI](preprocessing_dcm2nii)
     * [Align anterior commissure and posterior commisure](preprocessing_acpcdetect)
     * [Correct intensity nonuniformities (bias field)](preprocessing_N4BiasFieldCorrection)
     * [Resample images to isotropic voxel size 1](preprocessing_resample)
     * [Brain Extraction and Tissue Segmentation](preprocessing_antscorticalthickness)
4. Hippocampus Segmentation
     * [Placing Landmarks](hpc_landmarks)

---------------------------------------

Table of Contents:

[TOC]

---------------------------------------

The dcm2nii program converts DICOM files from your scanner into the NIfTI format that's used by many programs like: FSL, SPM, ANTs, etc. The NIfTI image format standard is the common standard used in scientific image processing, because the file is compact, simple, and versatile.

# Before you Begin

Organizing your files can take a lot of time and effort, but assuring that your files are organized properly will save you a lot of time and allow you to easily batch process many participants at once. Standard organization involves having a central data directory and under that data directory you will have a folder for each participant and finally under each participant all the files will be placed. For example the participant folder, `1222--03-23-09` is located under a main practice directory. Within the participant directory are all their DICOM folders organized by scan sequence:

![Screenshot.png](https://bitbucket.org/repo/pAjpdx/images/2724483552-Screenshot.png)

# Using preprocessing_dcm2nii for the first time

To run the program, you should be able to type in a new Terminal window to see the available options:

```
#!console
$ dcm2nii
Chris Rorden's dcm2nii :: 6 June 2013
reading preferences file /home/njhunsak/.dcm2nii/dcm2nii.ini
Either drag and drop or specify command line options:
  dcm2nii <options> <sourcenames>
OPTIONS:
-4 Create 4D volumes, else DTI/fMRI saved as many 3D volumes: Y,N = Y
-a Anonymize [remove identifying information]: Y,N = Y
-b load settings from specified inifile, e.g. '-b C:\set\t1.ini'  
-c Collapse input folders: Y,N = Y
-d Date in filename [filename.dcm -> 20061230122032.nii]: Y,N = Y
-e events (series/acq) in filename [filename.dcm -> s002a003.nii]: Y,N = Y
-f Source filename [e.g. filename.par -> filename.nii]: Y,N = N
-g gzip output, filename.nii.gz [ignored if '-n n']: Y,N = Y
-i ID  in filename [filename.dcm -> johndoe.nii]: Y,N = N
-m manually prompt user to specify output format [NIfTI input only]: Y,N = Y
-n output .nii file [if no, create .hdr/.img pair]: Y,N = Y
-o Output Directory, e.g. 'C:\TEMP' (if unspecified, source directory is used)
-p Protocol in filename [filename.dcm -> TFE_T1.nii]: Y,N = Y
-r Reorient image to nearest orthogonal: Y,N 
-s SPM2/Analyze not SPM5/NIfTI [ignored if '-n y']: Y,N = N
-v Convert every image in the directory: Y,N = Y
-x Reorient and crop 3D NIfTI images: Y,N = N
  You can also set defaults by editing /home/njhunsak/.dcm2nii/dcm2nii.ini
EXAMPLE: dcm2nii -a y /Users/Joe/Documents/dcm/IM_0116
``` 

# Converting all the DICOM images in participant directory

There are many options for you to use but here's the basic command you can use for your images:

```
#!console
$ dcm2nii -a y -g n -r n -x n -o ~/preprocessing-t1-example/1222_032309/ ~/preprocessing-t1-example/1222_032309/*
```

The `*` at the end of the input directory tells the program to process everything in the participant directory. If you don't place the `*` the program will give you an error:

```
#!console
$ dcm2nii -a y -g n -r n -x n -o ~/preprocessing-t1-example/1222_032309/ ~/preprocessing-t1-example/1222_032309/
Chris Rorden's preprocessing_dcm2nii :: 6 June 2013
reading preferences file /home/njhunsak/.dcm2nii/dcm2nii.ini
Data will be exported to /home/njhunsak/Desktop/1222--03-23-09/
An unhandled exception occurred at $000000000047F0DD :
EAccessViolation : Access violation
  $000000000047F0DD
  $000000000040E71A
  $000000000041F7E8
  $00000000004211C5
```

# Cropping and reorienting images

You can easily combine these two steps at once, but if for some reason you needed to go back and reprocess your NIfTI image, the preprocessing_dcm2nii program can. For this example, we will go back and crop and make sure the NIfTI image is in standard orientation:

```
#!console
$ dcm2nii -g n -x y -o ~/preprocessing-t1-example/1222_032309/ ~/preprocessing-t1-example/1222_032309/t1.nii
```

**Why reorient the image?**

> The NIfTI format stores spatial transforms so that software can determine the oreintation of the image. This means that MRIcron can display the image with an intuitive orientation. However, many programs ignore these transforms, and display the images as they are saved to disk (e.g. FSLview, MRIcro) - this means that a sagittally acquired scan appears very differently from an axially acquired scan. In fact, the three spatial dimensions (left-right, anterior-posterior, superior-inferior) can be saved in 48 different orthogonal orientations. A new copy of the image is created with the prefix 'o'.

**Why crop the image?**

> After reorienting, dcm2nii will attempt to 'autocrop' T1-weighted anatomical images (images with a Echo Time [TE] of less than 20ms). A new copy of the image is created with the prefix 'c' that attempts to remove excess air surrounding the individual as well as parts of the neck below the cerebellum. This excess neck can disrupt normalization of images (as the template images do not have similar neck regions). This new image has a slightly different NIfTI transform - the origin is adjusted to compensate for the removed portions of the image. 

### Notes

DICOM files need to have the .dcm file extension at the end of the file for dcm2nii to run properly. If you need to batch find files that do not have this extension and add the extension use the following code:

```
#!console
$ find /path/to/DICOM/directories/ -type f ! -name "*.*" -exec mv -v {} {}.dcm \;
```