For reference, your fixed image is your template and your moving image is your participant.

# ANTs Nonlinear Registration

In your command window, type:

```bash
antsRegistrationSyn.sh \
-d 3 \
-f <fixedImage>.nii.gz \
-m <movingImage>.nii.gz \
-o <outputPrefix> \
-t s
```

To run a quicker version, type:
```bash
antsRegistrationSynQuick.sh \
-d 3 \
-f <fixedImage>.nii.gz \
-m <movingImage>.nii.gz \
-o <outputPrefix>
-t s
```

Both of these commands are simplified shell scripts of the actual command `antsRegistration`. You can view the code in these scripts by running either:

```bash
cat /usr/local/antsbin/bin/antsRegistrationSyn.sh
cat /usr/local/antsbin/bin/antsRegistrationSynQuick.sh
```

One of the differences between the two commands is the number of iterations in the last iteration step. For antsRegistrationSynQuick.sh there are 0 iteractions and for antsRegistrationSyn.sh there are 100 iterations. The other difference is the metric used for registration. For antsRegistrationSynQuick.sh, the registration metric is based on mutual information (great for multimodal images). For antsRegistrationSyn.sh, the registration metric is based on cross correlation (great for T1 weighted image registration).

\newpage

# Generate Warped Images

```bash
# Make the participant image look like the template
WarpImageMultiTransform 3 \
<movingImage>.nii.gz \
<outputImage>.nii.gz \
<outputPrefix>Warp.nii.gz \
<outputPrefix>Affine.txt \
-R <fixedImage>.nii.gz

# Make the template look like the participant
WarpImageMultiTransform 3 \
<fixedImage>.nii.gz \
<outputImage>.nii.gz \
-i <outputPrefix>Affine.txt \
<outputPrefix>InverseWarp.nii.gz \
-R <movingImage>.nii.gz
```

# Generate the Grid Image

```bash
CreateWarpedGridImage 3 \
<outputPrefix>Warp.nii.gz \
<outputGrid>.nii.gz \
1x1x1 \ 
5x5x5 
```

# Generate the Jacobian

```bash
# Jacobian
CreateJacobianDeterminantImage 3 \
  <outputPrefix>Warp.nii.gz \
  <outputJac>.nii.gz \
  0 \ # Default
  1
  
# Log Jacobian
CreateJacobianDeterminantImage 3 \
  <outputPrefix>Warp.nii.gz \
  <outputLogJac>.nii.gz \
  1 \ # Take the log of the Jacobian  
  1
```

# Modulate the Gray Matter Image

```bash
c3d \
<inputImage>.nii.gz \
<jacobianImage>.nii.gz \
-multiply \
-o <modulatedImage>.nii.gz
```

If you have your tissue segmentation ROIs (see Preprocessing T1 example), then split the ROIs, so you just have a gray matter ROI. You will extract just the modulated GM from the brain image using this mask.

```bash
c3d \
<modulateImage>.nii.gz \
<gmMask>.nii.gz \
-multiply \
-o <outputImage>.nii.gz
```

# Evaluate Image Similarity

```bash
ImageMath \
3 \
<outputFile>.ext \
NormalizedCorrelation \
<image1>.nii.gz \
<image2>.nii.gz
```

# Further Readings

* Morphometry - http://www.fil.ion.ucl.ac.uk/spm/doc/books/hbf2/pdfs/Ch6.pdf
