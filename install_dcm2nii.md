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

The [installation guide](http://www.mccauslandcenter.sc.edu/mricro/mricron/install.html) can be found here.

# Linux

* Download the [latest version](http://www.mccauslandcenter.sc.edu/mricro/mricron/install.html). 

* Unzip the downloaded file (which currently produces a folder call `mricron`).

* Configure dcm2nii

```
#!console
# mv /home/<username>/Downloads/mricron/ /usr/local/
# ln -s /usr/local/mricron/dcm2nii /usr/local/bin/
```

# Mac

* Download the [latest version](http://www.nitrc.org/frs/download.php/5628/osx.zip).

* The zip file should automatically unzip and create a folder labeled `osx` in your Downloads folder or wherever your files automatically download.

* Move (drag and drop) the `osx` folder into your Applications directory.

* You can either launch the program directly from the terminal by typing the following:

```
#!console
$ /Applications/osx/dcm2nii
```

* If you want to be able to just type dcm2nii into your Terminal window, you can configure the program:

```
#!console
$ sudo ln -s /Applications/osx/dcm2nii /usr/bin/
```

# Windows

* Download the [latest version](http://www.nitrc.org/frs/download.php/5630/win.zip).

* Unzip the files to C:\Windows\Downloaded Program Files (which produces a folder titled "mricron").

* Edit environment variables to open mricron files from command prompt.

> Open Control Panel under the start menu > System and Security > System > Advanced system settings > Environmental Variables

> Under System Variables select PATH and edit

> Enter `;C:\Windows\Downloaded Program Files\mricron`