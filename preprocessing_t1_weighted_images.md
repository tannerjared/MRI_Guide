# Set Environment Variables

```bash
export ANTSPATH=/usr/local/antsbin/bin/
PATH=${ANTSPATH}:${PATH}
```

# Convert DICOM to NIfTI
	
```bash
$ dcm2nii \
-a y \
-g y \
-r y \
-x y \
-o <outputdirectory> \
<inputdirectory>/*
```
	
# Correct Bias Field

```bash
$ N4BiasFieldCorrection \
-d 3 \
-i <inputImage>.nii.gz \
-o [<correctedImage>.nii.gz,<biasfield>.nii.gz] \
-s 4 \ 
-b [200] \
-c [50x50x50x50,0.000001]
```

# Resample to 1 mm Isotropic

```bash
$ c3d \
-verbose \
<inputImage>.nii.gz \
-resample-mm 1x1x1mm \
-o <outputImage>.nii.gz
```
	
# Generate Tissue Segmentation & Cortical Thickness
## STOP THIS STEP TAKES 12+ HOURS!!!

```bash
$ antsCorticalThickness.sh \
-d 3 \
-a <inputImage>.nii.gz \
-a <multimodalImage>.nii.gz \ # optional
-e T_template0.nii.gz \
-t T_template0_BrainCerebellum.nii.gz \
-m T_template0_BrainCerebellumProbabilityMask.nii.gz \
-f T_template0_BrainCerebellumExtractionMask.nii.gz \
-p Priors2/priors%d.nii.gz \
-q 1 \
-o <outputDir>/
```

# Create Separate Files for Each Tissue Segmentation

```bash
$ c3d \
<inputImage>.nii.gz \
-split \
-oo seg_background.nii.gz \
seg_csf.nii.gz \
seg_gm.nii.gz \
seg_wm.nii.gz \
seg_bfa.nii.gz \
seg_bs.nii.gz \
seg_crbl.nii.gz
```

# *N* Tissue Segmentations

```bash
$ antsAtroposN4.sh \
-d 3 \
-a <T1w>.nii.gz \
-a <multimodalImage>.nii.gz \ # optional
-x <mask>.nii.gz \
-c <numberofSegmentationClasses> \ # typically 3 tissues (GM, WM, CSF)
-o <outputPrefix>\
-n 2 \
-m 2
```

# Affine Register T2 Weighted to T1 Weighted Image	

```bash
$ antRegistrationSynQuick.sh \
-d 3 \
-f <T1Image>.nii.gz \
-m <T2Image>.nii.gz \
-o <outputPrefix> \
-t a
```

# Homework
## Due on Monday, September 29th

The dataset for this class can be found on the ds214 NAS drive under `dataset`. The participants are:

```bash
$ ls /Volumes/byustudent/dataset/
1304_082907	1310_010208	1326_061810	2310_010709	2320_042310
1306_091707	1315_112808	1327_031011	2314_032709	2323_083110
1307_121807	1319_042009	2304_012808	2316_062409	2324_120810
1308_111207	1320_082409	2307_031708	2317_123009	2370_020111
```

There are 10 orthopedic controls and 10 TBI participants. Under each participant folder there are three files:

```bash
$ ls /Volumes/byustudent/dataset/1304_082907
acpc.nii	seg.nii.gz	t2.nii.gz
```
You will need to write a single script to do the following across ALL participants:

1. Bias correct the `acpc.nii` image
2. Reslice the n4 bias correct image to 1 mm isotropic
3. Register the T2w image to the acpc aligned, n4 bias corrected, resliced T1w image (whew!)

## Reference Manuals

* BYU MRI Guide - https://bitbucket.org/njhunsaker/byu-mri-guide/wiki/Home
* dcm2nii - http://www.mccauslandcenter.sc.edu/mricro/mricron/dcm2nii.html
* Convert3D - http://www.itksnap.org/pmwiki/pmwiki.php?n=Convert3D.Documentation
* ANTs - https://github.com/stnava/ANTsDoc/raw/master/ants2.pdf
* acpcdetect - https://www.nitrc.org/docman/view.php/90/917/acpcdetect.pdf

## Further Readings

* Segmentation - http://sourceforge.net/projects/advants/files/Documentation/atropos.pdf/download
* Bias Correction - http://dx.doi.org/10.1109/TMI.2010.2046908
* Cortical Thickness - http://dx.doi.org/10.1016/j.neuroimage.2014.05.044
* Registration - http://sourceforge.net/projects/advants/files/Documentation/antstheory.pdf/download
* Automatic Detection of AC/PC - http://dx.doi.org/10.1016/j.neuroimage.2009.02.030

## Examples

* ANTs Atropos and N4 Example - https://github.com/ntustison/antsAtroposN4Example
* ANTs Brain Extraction Example - https://github.com/ntustison/antsBrainExtractionExample
* ANTs Cortical Thickness Example - https://github.com/ntustison/antsCorticalThicknessExample