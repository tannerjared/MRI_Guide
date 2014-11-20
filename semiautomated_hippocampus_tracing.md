# Set Environment Variables

```bash
$ export ANTSPATH=/usr/local/antsbin/bin/
$ PATH=${ANTSPATH}:${PATH}
```

To permenantly change this, edit your `bash_profile`:

```bash
$ vi ~/.bash_profile
```

Press the `a` key to edit text file and add the text above. When you are done editing press the `esc` key. To save the file, type `:w` and hit enter. To quit the text editor, type `:q` and press enter.

# Generate a Brain Mask and Skull Stripped Brain

```bash
$ c3d <segmentationImage>.nii.gz -binarize -o <outputMask>.nii.gz
$ c3d <inputImage>.nii.gz <maskImage>.nii.gz -multiply -o <outputImage>.nii.gz
```

# Register Template to Participant Image Using Landmarks

## Set Parameters

```bash
$ FIX=<template>.nii.gz
$ FIXL=<templateLandmarks>.nii.gz
$ FIXM=<templateTracing>.nii.gz
$ MOV=<inputImage>.nii.gz
$ MOVL=<inputLandmarks>.nii.gz
$ OUT=<outputPrefix>
$ ITS=100x100x100x20
$ DIM=3
$ LMWT=0.9
$ INTWT=4
$ PCT=0.8
$ PARZ=100
$ LM=PSE[${FIX},${MOV},$FIXL,$MOVL,${LMWT},${PCT},${PARZ},0,25,10000]
$ INTENSITY=CC[$FIX,${MOV},${INTWT},4]
```

## Run ANTs

```bash
$ ANTS \
$DIM \
-o $OUT \
-i $ITS \
-t SyN[0.1] \
-r Gauss[3,0.] \
-m $INTENSITY \
-m $LM
```

## Warp Images
```bash
# Warp Participant to Template

WarpImageMultiTransform \
$DIM \
$MOV \
${OUT}ParticipanttoTemplate.nii.gz \
${OUT}Warp.nii.gz \
${OUT}Affine.txt \
-R $FIX

# Warp Template to Participant

$ WarpImageMultiTransform \
$DIM \
$FIX \
${OUT}TemplatetoParticipant.nii.gz \
-i ${OUT}Affine.txt \
${OUT}InverseWarp.nii.gz \
-R $MOV

# Warp Tracing to Participant

$ WarpImageMultiTransform \
$DIM \
$FIXM \
${OUT}auto.nii.gz \
-i ${OUT}Affine.txt \
${OUT}InverseWarp.nii.gz \
-R $MOV
```

# Exclude Everything NOT Gray Matter

```bash
$ c3d \
<autoSeg>.nii.gz \
<graymatter>.nii.gz \
-multiply \
-o <outputImage>.nii.gz
```

# Generate Learning Classifiers for Correcting Segmentation Errors

## STOP THIS STEP TAKES SEVERAL DAYS ON SOME COMPUTERS!!!

```bash
$ bl \
3 \
-ms *<manualSeg>.nii.gz \
-as *<autoSeg>.nii.gz \
-tl <targetLabel> \
<ouputPrefix>
```

# Apply Corrections to Segmentations

```bash
$ sa \
<autoSeg>.nii.gz \
<AdaBoost_outputPrefix> \
<outputImage>.nii.gz
```

# ROI Volume Overlap (AKA Dice's Coefficient)

Dice's Coefficient is defined as:

$$\frac{2 \times Volume(Manual \cap Automatic)}{Volume(Manual + Automatic)}$$

To calculate Dice's Coefficient:

```bash
$ c3d \
-verbose
<manualSeg>.nii.gz \
<autoSeg>.nii.gz \
-overlap <targetLabel>
```

# Extract Total Number of Voxels and Calculate Volume

```bash
$ fslstats \
<inputSegmentation>.nii.gz \
-l <1-targetLabel> \
-u <1+tagetLabel> \
-V
```

# Useful Code

## Save Output Values to Text File

At the end of the `c3d -overlap` or `fslstats` code add:

```bash
>> <outputFile>.txt
```

Use `TextWrangler.app` to edit your file into the standard *wide format* that can easily be imported into statistic software packages like SPSS, R, SAS, etc. In other words, each row represents data from one entity while each column represents a variable.

## Split an ROI into two ROIs

If you somehow get both the left and right hippocampus as a single ROI, there is a way to seperate the two ROIs:

```bash
$ val=$(fslval <inputSegmentation>.ni.gz dim1)
$ xsize=$(echo "$val/2" | bc)
$ fslroi <inputSegmentation>.ni.gz <outputLeft>.nii.gz 0 $xsize 0 -1 0 -1
$ xmin=$xsize; xsize=$(echo "$val-$xmin" | bc)
$ fslroi <inputSegmentation>.ni.gz <outputRight>.nii.gz $xmin $xsize 0 -1 0 -1
$ c3d <outputLeft>.nii.gz -binarize -o <outputLeft>.nii.gz
$ c3d <outputRight>.nii.gz -binarize -o <outputRight>.nii.gz
$ fslmaths <outputRight>.nii.gz -mul 2 <outputRight>.nii.gz
$ fslmerge -x <outputSegmentation>.nii.gz <outputRight>.nii.gz <outputLeft>.nii.gz
$ rm <outputRight>.nii.gz
$ rm <outputLeft>.nii.gz
```

# Homework

## Due on Monday, October 6, 2014

The dataset for this class located on the ds214 NAS drive now contains these files: n4_resliced.nii.gz, segmentation.nii.gz, t2.nii.gz, brain.nii.gz, HIP_auto.nii.gz, HIP_seg.nii.gz, HIP_manual.nii.gz

### Overall does any group show reduced right or left hippocampus volume?

Extract the volumes from the semi-automated hippocampus tracing (HIP_seg.nii.gz). Then, generate a plot comparing the two groups (13\* and 23\*) left hippocampus and right hippocampus.

### Does the hippocampus correlate with overall gray matter or total brain volume?

Next, from the segmentation file extract the gray matter volume and then total brain volume ($\text{gray matter} + \text{white matter}$). Correlate hippocampus volume with just gray matter volume and then total brain volume. 

Remember to make your graphs *pretty*: provide a title, label your x- and y-axis, color code your two groups, include the standard error on bar plots, etc.

# Further Readings

* Template-Based Hippocampus Segmentation - http://dx.doi.org/10.1002/hipo.20619
* Learning-Based Wrapper - http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3049832/