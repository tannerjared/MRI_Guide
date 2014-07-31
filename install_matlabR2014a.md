How to Process MRI Images:

1. [Beginner's Guide to Command-Line Interface](primer)
2. [Install Programs](Home)
3. Preprocessing T1 images
     * [Convert DICOM to NIfTI](dcm2nii)
     * [Align anterior commissure and posterior commisure](acpcdetect)
     * [Correct intensity nonuniformities (bias field)](N4BiasFieldCorrection)

---------------------------------------

[TOC]

---------------------------------------

# Linux

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

# Mac

# Windows