### Note

DICOM files need to have the .dcm file extension at the end of the file for dcm2nii to run properly. If you need to batch find files that do not have this extension and add the extension use the following code:

```
#!consol
find /path/to/DICOM/dirs/ -type f ! -name "*.*" -exec mv -v {} {}.dcm \;
```