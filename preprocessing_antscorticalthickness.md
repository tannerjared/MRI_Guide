How to Process MRI Images:

1. [Beginner's Guide to Command-Line Interface](begin_primer)
2. [How to Install Programs](Home)
	 * [Specific instructions for installing programs on Fulton Supercomputing Lab](https://bitbucket.org/njhunsaker/fsl)
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

Brain extraction is a necessary step in all neuroimaging processing pipelines and it absolutely critical before doing any three-tissue segmentation. Although there are many tools and options for acquiring brain extraction:

* [FSL BET](http://fsl.fmrib.ox.ac.uk/fsl/fslwiki/BET)
* [IDeA Lab BET](http://idealab.ucdavis.edu/software/skullstrip_t1.php)

Many of these tools fail when dealing with typical and atypical children brains and adult atypical MR images. An alternative brain extraction method is to use image registration. The current pipeline uses a script provided by the ANTs program. In it's most simplistic form, by registering a template image to each participant, we are able to acquire a rough brain mask. With a general brain mask, ANTs is able to refine it by doing three-tissue segmentation.

Three-tissue segmentation is when you parcellate the brain in gray matter, white matter, and CSF. Again, there are several other options for acquiring tissue segmentation automatically:

* [FSL FAST](http://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FAST)
* [SPM Image Segmentation](http://www.fil.ion.ucl.ac.uk/spm/doc/books/hbf2/pdfs/Ch5.pdf)

But again, tissue segmentation tends to reduce in accuracy with children brains and atypical adult brains. The ANTs program uses multiple approaches when acquiring tissue segmentation: cortical constraints and prior probabilities. By combing common sense cortical constraints and probability masks, they are able to again acquire much more robust tissue segmentation in populations with very variable MR images.

# Before you begin

You will need to set the environmental variables when you want to use the program:

```
#!console
$ export ANTSPATH=/usr/local/antsbin/bin/
$ PATH=${ANTSPATH}:${PATH}
```

# Using ANTs Cortical Thickness for the first time

To run the program, you should be able to type in a new Terminal window to see the available options:

```
#!console
$ antsCorticalThickness.sh 

antsCorticalThickness.sh performs T1 anatomical brain processing where the following steps are currently applied:

  1. Brain extraction
  2. Brain n-tissue segmentation
  3. Cortical thickness
  4. (Optional) registration to a template

Usage:

antsCorticalThickness.sh -d imageDimension
              -a anatomicalImage
              -e brainTemplate
              -m brainExtractionProbabilityMask
              -p brainSegmentationPriors
              <OPTARGS>
              -o outputPrefix

Example:

  bash /usr/local/antsbin/bin/antsCorticalThickness.sh -d 3 -a t1.nii.gz -e brainWithSkullTemplate.nii.gz -m brainPrior.nii.gz -p segmentationPriors%d.nii.gz -o output

Required arguments:

We use *intensity* to denote the original anatomical image of the brain.

We use *probability* to denote a probability image with values in range 0 to 1.

We use *label* to denote a label image with values in range 0 to N.

     -d:  Image dimension                       2 or 3 (for 2- or 3-dimensional image)
     -a:  Anatomical image                      Structural *intensity* image, typically T1.  If more than one
                                                anatomical image is specified, subsequently specified
                                                images are used during the segmentation process.  However,
                                                only the first image is used in the registration of priors.
                                                Our suggestion would be to specify the T1 as the first image.
     -e:  Brain template                        Anatomical *intensity* template (possibly created using a population
                                                data set with buildtemplateparallel.sh in ANTs).  This template is
                                                *not* skull-stripped.
     -m:  Brain extraction probability mask     Brain *probability* mask created using e.g. LPBA40 labels which
                                                have brain masks defined, and warped to anatomical template and
                                                averaged resulting in a probability image.
     -p:  Brain segmentation priors             Tissue *probability* priors corresponding to the image specified
                                                with the -e option.  Specified using c-style formatting, e.g.
                                                -p labelsPriors%02d.nii.gz.  We assume that the first four priors
                                                are ordered as follows
                                                  1:  csf
                                                  2:  cortical gm
                                                  3:  wm
                                                  4:  deep gm
     -o:  Output prefix                         The following images are created:
                                                  * /Users/mriresearch/Documents/byu-mri-guide/wiki//tmp7187//tmpBrainExtractionMask.nii.gz
                                                  * /Users/mriresearch/Documents/byu-mri-guide/wiki//tmp7187//tmpBrainSegmentation.nii.gz
                                                  * /Users/mriresearch/Documents/byu-mri-guide/wiki//tmp7187//tmpBrainSegmentation*N4.nii.gz One for each anatomical input
                                                  * /Users/mriresearch/Documents/byu-mri-guide/wiki//tmp7187//tmpBrainSegmentationPosteriors*1.nii.gz  CSF
                                                  * /Users/mriresearch/Documents/byu-mri-guide/wiki//tmp7187//tmpBrainSegmentationPosteriors*2.nii.gz  GM
                                                  * /Users/mriresearch/Documents/byu-mri-guide/wiki//tmp7187//tmpBrainSegmentationPosteriors*3.nii.gz  WM
                                                  * /Users/mriresearch/Documents/byu-mri-guide/wiki//tmp7187//tmpBrainSegmentationPosteriors*4.nii.gz  DEEP GM
                                                  * ...
                                                  * /Users/mriresearch/Documents/byu-mri-guide/wiki//tmp7187//tmpBrainSegmentationPosteriors*N.nii.gz where there are N priors
                                                  *                              Number formatting of posteriors matches that of the priors.
                                                  * /Users/mriresearch/Documents/byu-mri-guide/wiki//tmp7187//tmpCorticalThickness.nii.gz

Optional arguments:

     -s:  image file suffix                     Any of the standard ITK IO formats e.g. nrrd, nii.gz (default), mhd
     -t:  template for t1 registration          Anatomical *intensity* template (assumed to be skull-stripped).  A common
                                                use case would be where this would be the same template as specified in the
                                                -e option which is not skull stripped.
                                                We perform the registration (fixed image = individual subject
                                                and moving image = template) to produce the files.
                                                The output from this step is
                                                  * /Users/mriresearch/Documents/byu-mri-guide/wiki//tmp7187//tmpTemplateToSubject0GenericAffine.mat
                                                  * /Users/mriresearch/Documents/byu-mri-guide/wiki//tmp7187//tmpTemplateToSubject1Warp.nii.gz
                                                  * /Users/mriresearch/Documents/byu-mri-guide/wiki//tmp7187//tmpTemplateToSubject1InverseWarp.nii.gz
                                                  * /Users/mriresearch/Documents/byu-mri-guide/wiki//tmp7187//tmpTemplateToSubjectLogJacobian.nii.gz
     -f:  extraction registration mask          Mask (defined in the template space) used during registration
                                                for brain extraction.
     -k:  keep temporary files                  Keep brain extraction/segmentation warps, etc (default = 0).
     -i:  max iterations for registration       ANTS registration max iterations (default = 100x100x70x20)
     -w:  Atropos prior segmentation weight     Atropos spatial prior *probability* weight for the segmentation (default = 0.25)
     -n:  number of segmentation iterations     N4 -> Atropos -> N4 iterations during segmentation (default = 3)
     -b:  posterior formulation                 Atropos posterior formulation and whether or not to use mixture model proportions.
                                                e.g 'Socrates[1]' (default) or 'Aristotle[1]'.  Choose the latter if you
                                                want use the distance priors (see also the -l option for label propagation
                                                control).
     -j:  use floating-point precision          Use floating point precision in registrations (default = 0)
     -u:  use random seeding                    Use random number generated from system clock in Atropos (default = 1)
     -v:  use b-spline smoothing                Use B-spline SyN for registrations and B-spline exponential mapping in DiReCT.
     -r:  cortical label image                  Cortical ROI labels to use as a prior for ATITH.
     -l:  label propagation                     Incorporate a distance prior one the posterior formulation.  Should be
                                                of the form 'label[lambda,boundaryProbability]' where label is a value
                                                of 1,2,3,... denoting label ID.  The label probability for anything
                                                outside the current label

                                                  = boundaryProbability * exp( -lambda * distanceFromBoundary )

                                                Intuitively, smaller lambda values will increase the spatial capture
                                                range of the distance prior.  To apply to all label values, simply omit
                                                specifying the label, i.e. -l [lambda,boundaryProbability].

     -q:  Use quick registration parameters     If = 1, use antsRegistrationSyNQuick.sh as the basis for registration
                                                during brain extraction, brain segmentation, and (optional) normalization
                                                to a template.  Otherwise use antsRegistrationSyN.sh (default = 0).

     -z:  Test / debug mode                     If > 0, runs a faster version of the script. Only for testing. Implies -u 0.
                                                Requires single thread computation for complete reproducibility.
```

# ANTs Cortical Thickness

This process takes hours to run on a typical computer, so make sure you are able to press go and then not touch the computer until it has finished running. You will want to run in test / debug mode first by adding to your command-line `-z 1`.

```
#!console
$ cd ~/preprocessing-t1-example/1222_032309/
$ antsCorticalThickness.sh -d 3 \
  -a n4_resliced.nii.gz \
  -e OASIS-30_Atropos_template/T_template0.nii.gz \
  -t OASIS-30_Atropos_template/T_template0_BrainCerebellum.nii.gz \
  -m OASIS-30_Atropos_template/T_template0_BrainCerebellumProbabilityMask.nii.gz \
  -f OASIS-30_Atropos_template/T_template0_BrainCerebellumExtractionMask.nii.gz \
  -p OASIS-30_Atropos_template/Priors2/priors%d.nii.gz \
  -q 1 \
  -o antsCorticalThickness/
```        

## What you end up with

There's a long list of files after the script runs:

```
#!console
$ ls 
BrainExtractionBrain.nii.gz
BrainExtractionMask.nii.gz
BrainNormalizedToTemplate.nii.gz
BrainSegmentation0N4.nii.gz
BrainSegmentationConvergence.txt
BrainSegmentation.nii.gz
BrainSegmentationPosteriors1.nii.gz
BrainSegmentationPosteriors2.nii.gz
BrainSegmentationPosteriors3.nii.gz
BrainSegmentationPosteriors4.nii.gz
BrainSegmentationPosteriors5.nii.gz
BrainSegmentationPosteriors6.nii.gz
BrainSegmentationPriorInverseWarped.nii.gz
BrainSegmentationTiledMosaic.png
brainvols.csv
CorticalThickness.nii.gz
CorticalThicknessNormalizedToTemplate.nii.gz
CorticalThicknessTiledMosaic.png
ExtractedBrain0N4.nii.gz
ExtractedTemplateBrain.nii.gz
RegistrationTemplateBrainMask.nii.gz
SubjectToTemplate0GenericAffine.mat
SubjectToTemplate1Warp.nii.gz
SubjectToTemplateInverseWarped.nii.gz
SubjectToTemplateLogJacobian.nii.gz
TemplateToSubject0Warp.nii.gz
TemplateToSubject1GenericAffine.mat
```

To make things easier, I will copy the important files into my main participant directory:

```
#!console
$ cd ~/preprocessing-t1-example/1222_032309/
$ cp antsCorticalThickness/BrainExtractionBrain.nii.gz brain.nii.gz
$ cp antsCorticalThickness/BrainExtractionMask.nii.gz mask.nii.gz
$ cp antsCorticalThickness/BrainSegmentation.nii.gz tissue_segmentation.nii.gz
```

To do this in batch form:

```
#!console
$ for i in $(find ~/preprocessing-t1-example/ -type d -name "antsCorticalThickness"); do
> subjDir=$(dirname $i)
> cp $i/BrainExtractionBrain.nii.gz ${subjDir}/brain.nii.gz
> cp $i/BrainExtractionMask.nii.gz ${subjDir}/mask.nii.gz
> cp $i/BrainSegmentation.nii.gz ${subjDir}/tissue_segmentation.nii.gz
> done
```
                                         
### Note

* The templates require the full path to their directory and the <prefix> requires the full path to its desired directory. For example, the templates may need to have `shared/templates/OASIS-30_Atropos_template/desired_template`. If your running command line from where you want the created files to be made then you only need to type in the title you want to prefix each file it outputs.

* Atropos templates can be obtained [here](http://mindboggle.info/data/templates/atropos/OASIS-30_Atropos_template.tar.gz)

* Using this script is super helpful if you ever want to run shape analyses on cortical labels acquired from FreeSurfer. If you have a FreeSurfer dataset and this output from this script, you can run [MindBoggle](http://mindboggle.info/users/README.html).