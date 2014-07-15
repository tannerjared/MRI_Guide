[TOC]

# Before You Begin

You may need to be logged in as root to install many of these programs, depending on the permissions of the directory on which you are installing. The following are specifics about the operation system in which programs were installed: 

**Version Notes**

* Red Hat Enterprise Linux Server Release 6.2 (Santiago)


# Firefox

**Linux**

* Download Firefox 30 Archive

```
#!console
# cd /usr/local
# wget http://ftp.mozilla.org/pub/mozilla.org/firefox/releases/30.0/linux-x86_64/en-US/firefox-30.0.tar.bz2
```

* Extract Archive

```
#!console
# tar xvjf firefox-30.0.tar.bz2
```

* Configure Firefox

```
#!console
# ln -s /usr/local/firefox/firefox /usr/local/bin/firefox

```

**Mac**

**Windows**

* Download the [latest version](https://download.mozilla.org/?product=firefox-stub&os=win&lang=en-US).
* Run Firefox Setup

# dcm2nii DICOM to NIfTI conversion

The [installation guide](http://www.mccauslandcenter.sc.edu/mricro/mricron/install.html) can be found here.

**Linux**

* Download the [latest version](http://www.mccauslandcenter.sc.edu/mricro/mricron/install.html). 

* Unzip the downloaded file (which currently produces a folder call `mricron`).

* Configure dcm2nii

```
#!console
# mv /home/<username>/Downloads/mricron/ /usr/local/
# ln -s /usr/local/mricron/dcm2nii /usr/local/bin/
```

You can confirm that the program works by typing `dcm2nii` into the command terminal and pressing enter:

```
#!console
$ dcm2nii

Chris Rorden's dcm2nii :: 6 June 2013
reading preferences file /home/njhunsak/.dcm2nii/dcm2nii.ini
Either drag and drop or specify command line options:
  dcm2nii <options> <sourcenames>
OPTIONS:
-4 Create 4D volumes, else DTI/fMRI saved as many 3D volumes: Y,N = Y
-a Anonymize [remove identifying information]: Y,N = Y
-b load settings from specified inifile, e.g. '-b C:\set\t1.ini'  
-c Collapse input folders: Y,N = Y
-d Date in filename [filename.dcm -> 20061230122032.nii]: Y,N = Y
-e events (series/acq) in filename [filename.dcm -> s002a003.nii]: Y,N = Y
-f Source filename [e.g. filename.par -> filename.nii]: Y,N = N
-g gzip output, filename.nii.gz [ignored if '-n n']: Y,N = Y
-i ID  in filename [filename.dcm -> johndoe.nii]: Y,N = N
-m manually prompt user to specify output format [NIfTI input only]: Y,N = Y
-n output .nii file [if no, create .hdr/.img pair]: Y,N = Y
-o Output Directory, e.g. 'C:\TEMP' (if unspecified, source directory is used)
-p Protocol in filename [filename.dcm -> TFE_T1.nii]: Y,N = Y
-r Reorient image to nearest orthogonal: Y,N 
-s SPM2/Analyze not SPM5/NIfTI [ignored if '-n y']: Y,N = N
-v Convert every image in the directory: Y,N = Y
-x Reorient and crop 3D NIfTI images: Y,N = N
  You can also set defaults by editing /home/njhunsak/.dcm2nii/dcm2nii.ini
EXAMPLE: dcm2nii -a y /Users/Joe/Documents/dcm/IM_0116
```

**Mac**

**Windows**

* Download the [latest version](http://www.nitrc.org/frs/download.php/5630/win.zip).

* Unzip the files to C:\Windows\Downloaded Program Files (which produces a folder titled "mricron").

* Edit environment variables to open mricron files from command prompt.

> Open Control Panel under the start menu > System and Security > System > Advanced system settings > Environmental Variables

> Under System Variables select PATH and edit

>Enter `;C:\Windows\Downloaded Program Files\mricron`

* To ensure a proper download type `dcm2nii` into the command prompt and press enter. If it downloaded correctly you should see a similar output as the one listed above under the Linux version

# Multi-image Analysis GUI (MANGO)

The [installation guide](http://ric.uthscsa.edu/mango/mango.html) can be found here.

**Linux**

* Download the [latest version](http://ric.uthscsa.edu/mango/downloads/mango_unix.zip) here.

* Unzip the downloaded file (which currently produces a folder call `mango`).

```
#!console
# unzip /home/<username>/Downloads/mango_unix.zip -d /usr/local/
```

* Configure Mango

```
#!console
# /usr/local/Mango/mango
```

> Click Accept

> Go to Options > Install Utilities

> Location should be: /usr/local

> Click Install

> You should have the following files:

```
#!console
$ ls /usr/local/bin/
applytransform  convert2des  genheader  mango    vols2series
convert2avw     convert2nii  imageinfo  resizer
convert2dc      makeroi    roi2nii
```

You can confirm that the command-line utilities were installed correctly by typing:

```
#!console
$ mango
```

**Mac**

**Windows**

* Download the [latest version](http://ric.uthscsa.edu/mango/downloads/mango_windows.zip).
* Extract the mango installer (It doesn't really matter where you extract it to, as long as you can find it later)
* Run mango installer and when prompted to create a shortcut do so
* Place the mango shortcut in a directory and add an environment variable leading to it under PATH (For example, if you placed mango in the "Downloaded Program Files" path you would add `;C:\Windows\Downloaded Program Files` to PATH)
* To access mango from the command prompt type `start mango`

# MATLAB R2014a

**Linux**

* Unzip the downloaded file:

```
#!console
# unrar x /home/<username>/Downloads/R2014a_UNIX.rar /usr/local/matlab/
```

* If you have problems installing unrar:

```
#!console
# rpm -Uvh http://pkgs.repoforge.org/rpmforge-release/rpmforge-release-0.5.2-2.el6.rf.i686.rpm
# yum -y --enablerepo=rpmforge install unrar
```
* Change permissions on files before installing:

```
#!console
# cd /usr/local/matlab/
# chmod +x java/
# chmod +x install
# chmod a+x sys/java/jre/glnxa64/jre/bin/
```

* Install:
```
#!console
# ./install
```

> Choose Use a File Installation Key and click Next. 

> If you agree to the licensing terms, choose Yes and click Next.

> Choose I have the File Installation Key for my license and put in the Key from the Downloads area.

> Click Next.

> Keep the installation destination and click Next.

> Select the products to install and click Next.

> Choose the areas for program shortcuts and click Next.

> Review the installation summary and click Install.

> Additional installations may be required depending on the previous product selections. Follow the installation instructions.

> Make certain the check mark is in for Activate MATLAB and click Next.

> A new window will come up after a few moments. Choose Activate automatically using the Internet and click Next.

> Log on to your MathWorks Account or choose to create an account. The Activation Key from the downloads area will be needed to create an account.

> For the license, choose the TAH Designated Computer and click Next.

> Click Confirm to send the information to MathWorks.
 
> Activation is complete. Click Finish.


**Mac**

**Windows**

# ACPC Detect

**Linux**

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

* You can confirm that the program was installed corretly by typing:

```
#!console
$ acpcdetect
```

**Mac**

Only available for Linux systems.

**Windows**

Only available for Linux systems.

# Advanced Normalization Tools

ANTs requires several programs to be installed first:

## GIT

**Linux**

You can check to see if you have git installed already on your system:

```
#!console
$ git --version
git version 1.7.1
```

* If you need to install:

```
#!console
# yum install git
```

**Mac**

**Windows**

* Download the [latest version](http://git-scm.com/download/win).


## CMAKE

**Linux**

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

**Mac**

**Windows**

* Download the [latest version](http://www.cmake.org/files/v3.0/cmake-3.0.0-win32-x86.exe).
* Run the CMake installer (for this version it was referred to as "cmake-3.0.0-win32-x86" in my downloads).

> The welcome scree should open. Click *Next*.

> It then shows the license agreement. Click *I Agree*.

> Install options will appear. Select the Add *CMake to the system PATH for all users* and click next.

> Now choose the location you'd like to install CMake.

> Now click *Install*.


## C++ Compiler

**Linux**

You can check to see if you have a GCC complier installed already on your system:

```
#!console
$ gcc --version
gcc (GCC) 4.4.6 20110731 (Red Hat 4.4.6-3)
Copyright (C) 2010 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```

**Mac**

**Windows**

(Unfortunately, Windows doesn't come with a default C++ compiler. There are many ways to obtain a GCC compiler. Below I have outlined how to use MinGW to to obtain a GCC compiler that works for ANTs installation.)

* Download the [latest version](http://sourceforge.net/projects/mingw/files/latest/download?source=files).

---------------------------------------

**Linux**

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
$ ANTSPATH=/usr/local/antsbin/bin/
$ PATH=${ANTSPATH}:${PATH}
```

**Mac**

**Windows**

# Convert3D

Convert3D requires several programs to be installed first:

## CMAKE

**Linux**

You can check to see if you have cmake installed already on your system:

```
#!console
$ cmake --version
cmake version 3.0.0

CMake suite maintained and supported by Kitware (kitware.com/cmake).
```

**Mac**

**Linux**


## ITK

A PDF of the ITK manual can be found here: [http://www.itk.org/ItkSoftwareGuide.pdf](http://www.itk.org/ItkSoftwareGuide.pdf)

**Linux**

* Download the latest version of ITK:

```
#!console
# cd /usr/local/
# git clone git://itk.org/ITK.git
```

* Install ITK:

```
#!console
# mkdir ITK-build
# cd ITK-build
# ccmake ../ITK
```

* Configure ITK by pressing the "c" key. In order to speed up the build process, disable the compilation of the unit tests and examples. This is done with the variables `BUILD TESTING=OFF` and `BUILD EXAMPLES=OFF`. Each time you change a set of variables in CMake, it is necessary to proceed to another configuration step by hitting the "c" key.

* When no new options appear in CMake, you can proceed to generate Makefiles by hitting the "g" key.


**Mac**


**Windows**


---------------------------------------

**Linux**

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


**Mac**


**Windows**


# DICOM toolkit (DCMTK)

Installation instructions can be found here: [http://support.dcmtk.org/docs/file_install.html](http://support.dcmtk.org/docs/file_install.html)

**Linux**

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


**Mac**


**Windows**