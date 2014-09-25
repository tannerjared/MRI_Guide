How to Process MRI Images:

1. [Beginner's Guide to Command-Line Interface](begin_primer)
2. [How to Install Programs](Home)
	 * [Specific instructions for installing programs on Fulton Supercomputing Lab](fsl)
3. Preprocessing T1 images
     * [Download example files](https://bitbucket.org/njhunsaker/preprocessing-t1-example)
     * [Convert DICOM to NIfTI](preprocessing_dcm2nii)
     * [Align anterior commissure and posterior commisure](preprocessing_acpcdetect)
     * [Correct intensity nonuniformities (bias field)](preprocessing_N4BiasFieldCorrection)
     * [Resample images to isotropic voxel size 1](preprocessing_resample)
     * [Brain Extraction and Tissue Segmentation](preprocessing_antscorticalthickness)
4. Hippocampus Segmentation
     * [Placing Landmarks](hpc_landmarks)

---------------------------------------

Table of Contents:

[TOC]

---------------------------------------

MR Images are often acquired at different voxel sizes. The MR sequence can be different after scanner upgrades or changes can be made the sequence itself. Voxel sizes can also be different in the 3-planes (non-isotropic). Unless you are very very lucky to be working with a pristine dataset with all images acquired on the same scanner, using the same sequence, you will need to account for these differences, by normalizing across all images. There are inherent drawbacks that occur when you reslice your images, but these effects mostly impact fMRI and DTI data, not structural T1. The drawbacks are associated with the interpolation (algorithmic guessing) of how to combine or split voxels and what intensity value to attribute to them. For example, if you are trying to spilt a voxel into two voxels right at a border between gray and white matter, how are you to know the intensity levels of the two new voxels? The take home message is don't reslice your data unless you have to and limit reslicing to structural images, avoid reslicing fMRI data.

# Using Convert3D for the first time

To run the program, you should be able to type in a new Terminal window to see the available options:

```
#!console
$ c3d -h

Command Listing:
    -accum
    -add
    -align-landmarks, -alm
    -anisotropic-diffusion, -ad
    -antialias, -alias
    -as, -set
    -background
    -biascorr
    -binarize
    -centroid
    -clear
    -clip
    -colormap, -color-map
    -connected-components, -connected, -comp
    -coordinate-map-voxel, -cmv
    -coordinate-map-physical, -cmp
    -copy-transform, -ct
    -create
    -dilate
    -divide
    -dup
    -endaccum
    -endfor
    -erode
    -erf
    -exp
    -fft
    -flip
    -foreach
    -glm
    -hessobj, -hessian-objectness
    -histmatch, -histogram-match
    -holefill, -hf
    -info
    -info-full
    -insert, -ins
    -interpolation, -interp, -int
    -iterations
    -label-overlap
    -label-statistics, -lstat
    -landmarks-to-spheres, -lts
    -laplacian, -laplace
    -levelset
    -levelset-curvature
    -levelset-advection
    -ln, -log
    -log10
    -max, -maximum
    -mcs, -multicomponent-split
    -mean
    -merge
    -mi, -mutual-info
    -min, -minimum
    -mixture, -mixture-model
    -multiply, -times
    -n4, -n4-bias-correction
    -ncc, -normalized-cross-correlation
    -nmi, -normalized-mutual-info
    -nlw, -normwin, -normalize-local-window
    -normpdf
    -noround
    -nospm
    -o
    -omc, -output-multicomponent
    -oo, -output-multiple
    -orient
    -origin
    -origin-voxel
    -overlap
    -overlay-label-image, -oli
    -pad
    -percent-intensity-mode, -pim
    -pixel
    -pop
    -popas
    -probe
    -push, -get
    -rank
    -reciprocal
    -region
    -reorder
    -replace
    -resample
    -resample-mm
    -reslice-itk
    -reslice-matrix
    -reslice-identity
    -rms
    -round
    -scale
    -set-sform
    -shift
    -signed-distance-transform, -sdt
    -slice
    -smooth
    -spacing
    -split
    -sqrt
    -staple
    -spm
    -stretch
    -subtract
    -test-image
    -test-probe
    -threshold, -thresh
    -tile
    -trim
    -trim-to-size
    -type
    -verbose
    -version
    -vote
    -vote-label
    -voxel-sum
    -voxel-integral, -voxel-int
    -voxelwise-regression, -voxreg
    -warp
    -wrap
    -weighted-sum, -wsum
    -weighted-sum-voxelwise, -wsv
```

# Reslice images to isotropic voxel size 1

The code is easy and straight-forward:

```
#!console
$ c3d ~/preprocessing-t1-example/1222_032309/n4.nii.gz -resample-mm 1x1x1mm -o ~/preprocessing-t1-example/1222_032309/n4_resliced.nii.gz
```