How to Process MRI Images:

1. [Beginner's Guide to Command-Line Interface](primer)
2. [Install Programs](Home)
3. Preprocessing T1 images
     * [Convert DICOM to NIfTI](dcm2nii)
     * [Align anterior commissure and posterior commisure](acpcdetect)
     * [Correct intensity nonuniformities (bias field)](N4BiasFieldCorrection)

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

* Download the latest version:

```
#!console
# cd /usr/local/
# wget http://www.cmake.org/files/v3.0/cmake-3.0.0.tar.gz
```

* Unzip the downloaded file:

```
#!console
# tar xzf cmake-3.0.0.tar.gz
```

* Configure, compile, and install:

```
#!console
# cd cmake-3.0.0
# ./configure --prefix=/usr/local && make && make install
```

# Mac

* Download the dmg file from [here](http://www.cmake.org/cmake/resources/software.html).

* Open the dmg file to run the installer.

* You should only have to drag and drop the app into the Application folder. 

* Open the CMake.app and go to Tools > Install For Command Line Use. You will need to make sure you have admin permissions.

# Windows

* Download the [latest version](http://www.cmake.org/files/v3.0/cmake-3.0.0-win32-x86.exe).
* Run the CMake installer (for this version it was referred to as "cmake-3.0.0-win32-x86" in my downloads).

> The welcome scree should open. Click *Next*.

> It then shows the license agreement. Click *I Agree*.

> Install options will appear. Select the Add *CMake to the system PATH for all users* and click next.

> Now choose the location you'd like to install CMake.

> Now click *Install*.

* Go to the *Installation* tab and select *Apply Changes*
