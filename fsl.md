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

Table of Contents:

[TOC]

---------------------------------------

There are specific issues with installing programs on the Fulton Supercomputing Lab. After logging into your account, create a bin directory within your home directory:

```
#!console
$ pwd
/fslhome/<username>
$ mkdir bin
$ cd bin
$ pwd
/fslhome/<username>/bin
```

# Advanced Normalization Tools

Under your bin directory, download the latest version of ANTs:

```
#!console
$ git clone git://github.com/stnava/ANTs.git
```

Install ANTs:

```
#!console
$ module load cmake/2.8.10.2 
$ mkdir antsbin
$ cd antsbin
$ ccmake ../ANTs
```

Configure ANTs by pressing the "c" key. Continue pressing "c" until no new options appear. When no new options appear in CMake, you can proceed to generate Makefiles by hitting the "g" key. Back in your terminal window:

```
#!console
$ make -j 4
```

and wait awhile.

You'll also need to copy the scripts into your new antsbin directory

```
cp /fslhome/<username>/bin/ANTs/Scripts/* /fslhome/<username>/bin/antsbin/bin/
```

Your ANTSPATH will be slightly different and needs to be included in all scripts:

```
#!console
$ export ANTSPATH=/fslhome/<username>/bin/antsbin/bin/
$ PATH=${ANTSPATH}:${PATH}
```

# ITK

Under your bin directory, download the latest version of ITK:

```
#!console
$ git clone git://itk.org/ITK.git
```

Install ITK:

```
#!console
$ module load cmake/2.8.10.2
$ mkdir ITK-build
$ cd ITK-build
$ ccmake ../ITK
```

Configure ITK by pressing the "c" key. In order to speed up the build process, disable the compilation of the unit tests and examples. This is done with the variables `BUILD TESTING=OFF` and `BUILD EXAMPLES=OFF`. Each time you change a set of variables in CMake, it is necessary to proceed to another configuration step by hitting the "c" key.
When no new options appear in CMake, you can proceed to generate Makefiles by hitting the "g" key.

```
#!console
$ make
```

# SegAdapter

Under your bin directory, download the latest version of SegAdapter:

```
#!console
$ module load cmake/2.8.10.2 
$ wget http://www.nitrc.org/frs/download.php/5859/segAdapter_1.9_release.tar.gz
$ tar -xzvf segAdapter_1.9.tar.gz
$ cd segAdapter_1.9_release/
```

You will need to edit the CMakeList.txt file:

```
#!console
$ vi CMakeLists.txt
```

To edit the text, press "a". You will need to change the following:

> TARGET_LINK_LIBRARIES(sa ITKNumerics ITKIO ITKStatistics)    
> TARGET_LINK_LIBRARIES(bl ITKNumerics ITKIO ITKStatistics)

To:

> TARGET_LINK_LIBRARIES(sa ${ITK_LIBRARIES})    
> TARGET_LINK_LIBRARIES(bl ${ITK_LIBRARIES})

When you are done editing your file, press the "esc" key. To save the file, press ":w" and to quit out of your text editor enter ":q".

Install SegAdapter:

```
#!console
$ ccmake .
```

Configure SegAdapter by pressing the "c" key. You need to change the variable `ITK_DIR` to `/fslhome/<username>/bin/ITK-build`. Each time you change a set of variables in CMake, it is necessary to proceed to another configuration step by hitting the "c" key.

```
#!console
$ make
```

You will need to provide the full pathname to run the SegAdapter:

```
#!console
$ /fslhome/intj5/bin/segAdapter_1.9_release/bl
$ /fslhome/intj5/bin/segAdapter_1.9_release/sa
```

# acpcdetect

Under your bin directory, download the latest version of acpcdetect:

```
#!console
$ mkdir art
$ cd art
$ wget http://www.nitrc.org/frs/download.php/6494/acpcdetect.tar.gz
$ tar -xvzf acpcdetect.tar.gz 
```

You need to set your $ARTHOME environment variable in all scripts:

```
#!console
$ ARTHOME=/fslhome/<username>/bin/art
$ export ARTHOME
```