### Note

DICOM files need to have the .dcm file extension at the end of the file for dcm2nii to run properly. If you need to batch find files that do not have this extension and add the extension use the following code:

```
#!console
$ find /path/to/DICOM/dirs/ -type f ! -name "*.*" -exec mv -v {} {}.dcm \;
```

You will also have to include the *.dcm file extension when trying to find files to convert:

```
#!console
$ dcm2nii -o ~/Desktop/1203--12-08-07/ /shared/ohio/mri/Cleveland/1203--12-08-07/dicom/*/*.dcm
```