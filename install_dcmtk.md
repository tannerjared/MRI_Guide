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

Installation instructions can be found here: [http://support.dcmtk.org/docs/file_install.html](http://support.dcmtk.org/docs/file_install.html)

# Linux

* Download the latest version of dcmtk:

```
#!console
# cd /usr/local/
# wget ftp://dicom.offis.de/pub/dicom/offis/software/dcmtk/dcmtk360/dcmtk-3.6.0.tar.gz
```

* Extract Archive

```
#!console
# tar xvzf dcmtk-3.6.0.tar.gz
```

* Configure:

```
#!console
# cd dcmtk-3.6.0
# ./configure
```
* Build the libraries and executables:

```
#!console
# make all
```

* Install the executables and some support files (data dictionary):

```
#!console
# make install
```

# Mac

# Windows