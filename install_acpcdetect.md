How to Process MRI Images:

1. [Beginner's Guide to Command-Line Interface](begin_primer)
2. [How to Install Programs](Home)
	 * [Specific instructions for installing programs on Fulton Supercomputing Lab](fsl)
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

---------------------------------------

# Linux

* Download the [latest version](http://www.nitrc.org/frs/?group_id=90) here.

* Unpack the package:

```
#!console
# cd /usr/local/
# mkdir art
# cd art/
# mv /home/<username>/Downloads/acpcdetect.tar.gz /usr/local/art/
# gunzip acpcdetect.tar.gz
# tar xvf acpcdetect.tar
# mv /usr/local/art/acpcdetect /usr/local/bin/
```

* Set the environmental variables:

```
#!console
$ ARTHOME=/usr/local/art
$ export ARTHOME
```

* You can confirm that the program was installed correctly by typing:

```
#!console
$ acpcdetect
```

# Mac

Only available for Linux systems.

# Windows

Only available for Linux systems.