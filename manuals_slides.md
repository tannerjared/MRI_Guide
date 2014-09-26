How to Process MRI Images:

1. [Beginner's Guide to Command-Line Interface](begin_primer)
2. Installation Instructions
    * [Programs](Home)
    * [Fulton Supercomputing Lab specific instructions](fsl)
3. Preprocessing T1 images
     * [Download example files](https://bitbucket.org/njhunsaker/preprocessing-t1-example)
     * [Convert DICOM to NIfTI](preprocessing_dcm2nii)
     * [Align anterior commissure and posterior commisure](preprocessing_acpcdetect)
     * [Correct intensity nonuniformities (bias field)](preprocessing_N4BiasFieldCorrection)
     * [Resample images to isotropic voxel size 1](preprocessing_resample)
     * [Brain Extraction and Tissue Segmentation](preprocessing_antscorticalthickness)
4. Hippocampus Segmentation
     * [Placing Landmarks](hpc_landmarks)

* [Reading Materials and Lecture Slides] (manuals_slides)

---------------------------------------

Reference Manuals

* [dcm2nii](http://www.mccauslandcenter.sc.edu/mricro/mricron/dcm2nii.html)

* [Convert3D](http://www.itksnap.org/pmwiki/pmwiki.php?n=Convert3D.Documentation)

* [ANTs](https://github.com/stnava/ANTsDoc/raw/master/ants2.pdf)

* [acpcdetect](https://www.nitrc.org/docman/view.php/90/917/acpcdetect.pdf)

Further Readings

* [Segmentation](http://sourceforge.net/projects/advants/files/Documentation/atropos.pdf/download)

* [Bias Correction](http://dx.doi.org/10.1109/TMI.2010.2046908)

* [Cortical Thickness](http://dx.doi.org/10.1016/j.neuroimage.2014.05.044)

* [Registration](http://sourceforge.net/projects/advants/files/Documentation/antstheory.pdf/download)

* [Automatic Detection of AC/PC](http://dx.doi.org/10.1016/j.neuroimage.2009.02.030)

Examples

* [ANTs Atropos and N4 Example](https://github.com/ntustison/antsAtroposN4Example)

* [ANTs Brain Extraction Example](https://github.com/ntustison/antsBrainExtractionExample)

* [ANTs Cortical Thickness Example](https://github.com/ntustison/antsCorticalThicknessExample)