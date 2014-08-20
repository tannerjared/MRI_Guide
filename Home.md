How to Process MRI Images:

1. [Beginner's Guide to Command-Line Interface](begin_primer)
2. [Install Programs](Home)
3. Preprocessing T1 images
     * [Download example files](https://bitbucket.org/njhunsaker/preprocessing-t1-example)
     * [Convert DICOM to NIfTI](dcm2nii)
     * [Align anterior commissure and posterior commisure](acpcdetect)
     * [Correct intensity nonuniformities (bias field)](N4BiasFieldCorrection)
     * [Brain Extraction and Tissue Segmentation](antscorticalthickness)
4. Hippocampus Segmentation
     * [Placing Landmarks](hpc_landmarks)

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

For those of you who are using Windows I would strongly encourage you not to. While some of these programs (MANGO, dcmi2nii, mricron, and some executive functions of ANTS) can be installed onto Windows easily, you will quickly find barriers between programs. The scientific community likes to run things on Linux. While Mac has been known to be accomodating for Linux type programs, Windows would rather kill you and your entire family before letting you fully install some of these programs. Because Windows isn't designed for running many of these it will slow your computer down drastically. Beneath you will find installation instructions for Windows up untill my computer became too slow to use. If you are interested in having these programs on your own computer I would suggest a free installation of Linux. [Here](http://www.ubuntu.com/download/server/install-ubuntu-server) you will find instructions on downloading Ubuntu, a free Linux operating system. It's quite easy and if you aren't fully commited to using just Linux you can partition your drive, which allows you to run Linux or Windows upon restarting your computer each time.

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