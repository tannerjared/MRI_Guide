# dcm2nii

The dcm2nii program converts DICOM files from your scanner into the NIfTI format that's used by many programs like: FSL, SPM, ANTs, etc. The NIfTI image format standard is the common standard used in scientific image processing, because the file is compact, simple, and versatile.

To run the program, you should be able to type in a new Terminal window to see the available options:

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
There are many options for you to use but here's the basic command you can use for your images:

```
#!console
$ dcm2nii -a y -g n -r n -x n -o ~/<subjDir>/ ~/<subjDir>/*
```

**Notes**

DICOM files need to have the .dcm file extension at the end of the file for dcm2nii to run properly. If you need to batch find files that do not have this extension and add the extension use the following code:

```
#!console
$ find /path/to/DICOM/dirs/ -type f ! -name "*.*" -exec mv -v {} {}.dcm \;
```