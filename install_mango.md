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

The [installation guide](http://ric.uthscsa.edu/mango/mango.html) can be found here. You can either download the latest version (v3.2.1) or previous versions. The current version (v3.2.x) does not seem to run quite like is has in the past, so we are currently using version 3.1.x.

# Linux

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

# Mac

* You can find the downloads page [here](http://ric.uthscsa.edu/mango/mango.html).

* Open (double-click) the `mango installer.pkg` to install the program.

* If you want to install command-line options, open the Mango.app and go to Options > Install Utilities… and then click Install. The program automatically installs the folder at /Users/<username>/bin/, but you need to move those files in that directory to /usr/bin:

```
#!
$ sudo mv /Users/<username>/bin/* /usr/bin/
$ rmdir /Users/<username>/bin
```

# Windows

* You can find the downloads page [here](http://ric.uthscsa.edu/mango/mango.html).

* Extract the mango installer (It doesn't really matter where you extract it to, as long as you can find it later)

* Run mango installer and when prompted to create a shortcut do so

* Place the mango shortcut in a directory and add an environment variable leading to it under PATH (For example, if you placed mango in the "Downloaded Program Files" path you would add `;C:\Windows\Downloaded Program Files` to PATH)

* To access mango from the command prompt type `start mango`