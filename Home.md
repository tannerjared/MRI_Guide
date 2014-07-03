[TOC]

# Version Notes

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
# ln -s /usr/local/firefox/firefox /usr/bin/firefox

```

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

> Location should be: /usr/local/bin

> Click Install

> You should have the following files:

```
#!console
$ ls /usr/local/bin/
applytransform  convert2des  genheader  mango    vols2series
convert2avw     convert2nii  imageinfo  resizer
convert2dc      makeroi    roi2nii
```

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

# ACPC Detect

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
# ARTHOME=/usr/local/art
# export ARTHOME
```

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
---------------------------------------

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
 