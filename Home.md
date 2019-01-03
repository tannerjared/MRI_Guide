How to Process MRI Images:

1. [Beginner's Guide to Command-Line Interface](begin_primer)
2. Installation Instructions
    * [Programs](Home)
    * [Fulton Supercomputing Lab specific instructions](fsl)
3. Preprocessing T1 images
     * [Download example files](https://bitbucket.org/njhunsaker/preprocessing-t1-example)
     * [Convert DICOM to NIfTI](preprocessing_dcm2nii)
     * [Align anterior commissure and posterior commisure](preprocessing_acpcdetect)
     * [Correct intensity nonuniformities (bias field)](preprocessing_N4BiasFieldCorrection)
     * [Resample images to isotropic voxel size 1](preprocessing_resample)
     * [Brain Extraction and Tissue Segmentation](preprocessing_antscorticalthickness)
4. Hippocampus Segmentation
     * [Placing Landmarks](hpc_landmarks)

[Reading Materials and Lecture Slides](manuals_slides)

---------------------------------------

# Before You Begin

You may need to be logged in as root to install many of these programs, depending on the permissions of the directory on which you are installing. The following are specifics about the operation system in which programs were installed: 

**Version Notes**

* Mac OS X Lion (10.7)
     * You should install Xcode first before beginning any of these other tasks. Depending on your OS version, [Xcode 4.6 was installed](https://developer.apple.com/downloads/index.action#)
     * In order to have access to root user you have to directly enable the option, [for instructions refer to this page here](http://support.apple.com/kb/ht1528).
* Red Hat Enterprise Linux Server Release 6.2 (Santiago)
* Windows 7 (If you are using Windows it may be easier to log in as the Administrator for all of these downloads)

**Attention Windows Users**

Some of these programs (MANGO, dcmi2nii, mricron, and some executive functions of ANTS) can be installed onto Windows easily, you will quickly find barriers between programs. The scientific community likes to run things on Linux. If you are interested in having these programs on your own computer I would suggest a free installation of Linux. Ubuntu, Mint, Debian, CentOS, and others work well. Ubuntu is quite easy and if you aren't fully commited to using just Linux you can run it in a Virtual Machine or partition your drive, which allows you to run Linux or Windows upon restarting your computer each time.

* [Firefox](install_firefox)
* [DICOM Toolkit](install_dcmtk)
* [dcm2nii DICOM to NIfTI conversion](install_dcm2nii)
* [Multi-image Analysis GUI (MANGO)](install_mango)
* [MATLAB R2014a](install_matlabR2014a)
* [ACPC Detect](install_acpcdetect)
* [Git](install_git)
* [CMake](install_cmake)
* [C++ Compiler](install_gcc)
* [Advanced Normalization Tools](install_ants)
* [ITK](install_itk)
* [Convert3D](install_convert3d)
