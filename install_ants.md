How to Process MRI Images:

1. [Beginner's Guide to Command-Line Interface](primer)
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

ANTs requires several programs to be installed first: [git](install_git), [cmake](install_cmake), and [C++ compiler](install_gcc).

# Linux

* Download the latest version of ANTs:

```
#!console
# cd /usr/local/
# git clone git://github.com/stnava/ANTs.git
```

* Install ANTs:

```
#!console
# mkdir antsbin
# cd antsbin
# ccmake ../ANTs
```

* Go into cmake and type “c” and then “g”  then exit back to the
terminal

```
#!console
# make -j 4
```

* Configure ANTs:

```
#!console
# cp  /usr/local/ANTs/Scripts/*  /usr/local/antsbin/bin/
$ export ANTSPATH=/usr/local/antsbin/bin/
$ PATH=${ANTSPATH}:${PATH}
```

# Mac

* Download the latest version of ANTs:

```
#!console
# cd /usr/local/
# git clone git://github.com/stnava/ANTs.git
```

* Install ANTs:

```
#!console
# mkdir antsbin
# cd antsbin
# ccmake ../ANTs
```

* Go into cmake and type “c” and then “g”  to exit back to the
terminal:

```
#!console
# make -j 4
```

* Configure ANTs:

```
#!console
# cp  /usr/local/ANTs/Scripts/*  /usr/local/antsbin/bin/
$ export ANTSPATH=/usr/local/antsbin/bin/
$ PATH=${ANTSPATH}:${PATH}
```

# Windows