How to Process MRI Images:

1. [Beginner's Guide to Command-Line Interface](begin_primer)
2. [Install Programs](Home)
3. Preprocessing T1 images
     * [Download example files](https://bitbucket.org/njhunsaker/preprocessing-t1-example)
     * [Convert DICOM to NIfTI](preprocessing_dcm2nii)
     * [Align anterior commissure and posterior commisure](preprocessing_acpcdetect)
     * [Correct intensity nonuniformities (bias field)](preprocessing_N4BiasFieldCorrection)
     * [Reslice images to isotropic voxel size 1](preprocessing_reslice)
     * [Brain Extraction and Tissue Segmentation](preprocessing_antscorticalthickness)
4. Hippocampus Segmentation
     * [Placing Landmarks](hpc_landmarks)

---------------------------------------

* [Firefox](install_firefox)
* [DICOM Toolkit](install_dcmtk)
* [preprocessing_dcm2nii DICOM to NIfTI conversion](install_preprocessing_dcm2nii)
* [Multi-image Analysis GUI (MANGO)](install_mango)
* [MATLAB R2014a](install_matlabR2014a)
* [ACPC Detect](install_preprocessing_acpcdetect)
* [Git](install_git)
* [CMake](install_cmake)
* [C++ Compiler](install_gcc)
* [Advanced Normalization Tools](install_ants)
* [ITK](install_itk)
* [Convert3D](install_convert3d)

---------------------------------------

# Linux

You can check to see if you have a GCC complier installed already on your system:

```
#!console
$ gcc --version
gcc (GCC) 4.4.6 20110731 (Red Hat 4.4.6-3)
Copyright (C) 2010 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```

# Mac

Open you Xcode.app and go to Xcode > Preferences > Downloads. Click to make sure you have the command line toolbox installed.


# Windows

(Unfortunately, Windows doesn't come with a default C++ compiler. There are many ways to obtain a GCC compiler. You may also find that your windows computer doesn't come with many other programs that are important for running the cmake process. This is the sensible place to stop downloading things in Windows if you value your sanity. Otherwise you will need to make sure you have Ruby, Python, SWIG, and possibly some other programs.)
