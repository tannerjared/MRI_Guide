# Statistical Analyses with SPM / MATLAB

## Smooth Images

* Select all the jacobian images that need to be smoothed.
* Either use the default or adjust the FWHM (blur intensity). With too little blur, you won't have enough voxels to form a significant cluster and with too much blur, you might washout significant clusters.

## Factorial Design Specification

* Select an output directory.
* Select statistical design (re: two-sample t-test).
* Select Group 1 scans (preferablly the control group).
* Select Group 2 scans.
* Select an explicit mask.

## Model Estimation

* Select SPM.mat file that contains the design specification.

## Contrast Manager

* Select SPM.mat file for contrasts
* Select New: T-contrast

### Contrast 1

* Set name to TD > TBI
* Set T contrast vector to 1 -1
* Select New: T-contrast

### Contrast 2

* Set name to TBI > TD
* Set T constrast vector to -1 1

## Results Report

* Select SPM.mat file that contains the design specification.
* Select New: Contrast Query
* Set results title to TD vs. TBI
* Set Contrast(s) to inf
* Set Threshold type to none
* Set Threshold to 0.001

## View Results in BrainNet Viewer

* Select general surface file like BrainMesh_ICBM152.nv
* Select volume file (re: SPM contrast file, spmT_0001.img or spmT_0002.img)
* Select layout to full view if you want a jpeg image, select layout to single view if you want a movie.

## Extract Binary ROI

* Select Results
  * Select contrasts... and follow prompts
  * Select the cluster from which you want to make a binary ROI
  * Select save > current cluster

## Identify Brain Structures

```matlab
# In MATLAB
[oneline,cellarray]=cuixuFindStructure([4 -40 19]);

# Use either code below to output the structures
oneline{1}
cellarray
```

# Extract Values

```bash
cd <PathToData>
for var in $(ls sjac*); do
    c3d -verbose $var <binaryROI>.img -label-statistics \
    >> <outputDir>/results.txt
done
```

# Homework

## Due on Monday, October 27, 2014

Write a statistic method and result section comparing controls versus severe TBI participants. Here's some example text you can use to draft your results section:

> Data were analyzed using Statistical Parametric Mapping 8 software (SPM8) running on MATLAB 2013b. Jacobian maps were smoothed with an 8-mm isotropic full-width at half maximum (FWHM) Gaussian kernel in order to improve signal-to-noise ratio. Using these smooth Jacobian maps, we performed voxel-wise statistical analysis between groups using a two-sample T-test in order to identify changes in brain regions. SPM t-contrast maps were generated using a threshold of p < 0.001. Significance levels for the t statistic were controlled by the false discovery rate (FDR) for multiple comparisons and we report clusters that exceeded a threshold of 100 voxels and correct cluster level at p < 0.05. Anatomical localization of the cerebral areas was defined by an expericed observer, using the MNI atlas. Table x presents the regions of significant regional reduction in severe TBI participants compared to controls. Compared to controls, the severe TBI group showed significant regional reduction in the parietal lobe, [...] (see Figure x). Table y presents the regions of significant regional expansion in severe TBI participants compared to controls. Compared to controls, the severe TBI group showed significant regional enlargement of the lateral ventricles, [...] (see Figure y).

Table x: Regional reduction in TBI compared to controls

--------------------------------|-------------|---------------|----------------|
Brain Area                      | Cluster (k) | Voxel Z score | MNI Coordinate |
--------------------------------|-------------|---------------|-----------|
Splenium of the Corpus Callosum | 61          | 5.31 | 4, -40, 19 |