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

Convert3D requires several programs to be installed first: [cmake](install_cmake) and [ITK](install_itk). You can double check that cmake was installed:

```
#!console
$ cmake --version
```

# Linux

* Download the latest version of Convert3D:

```
#!console
# cd /usr/local/
# wget http://sourceforge.net/projects/c3d/files/latest/download
```

* Extract Archive

```
#!console
# tar xvzf c3d-nightly-Linux-x86_64.tar.gz
```

* Configure Convert3D:

```
#!console
# mv -i /usr/local/c3d-1.0.0-Linux-x86_64/bin/* /usr/local
```

# Mac

* Download the latest version of Convert3D:

```
#!console
# cd /usr/local/
# wget http://sourceforge.net/projects/c3d/files/latest/download
```

* Run the installer

# Windows