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

The goal of this protocol is to place 6 ROIs (regions of interest) in the hippocampus of each hemisphere. 
These ROIs will be linked together and distinguished by color.

STEP BY STEP INSTRUCTIONS

1. Select desired structural Nifti file (“.nii”) in Finder and double click to open in Mango software.
 
2. Under the “Window” tab in the top left corner of the image, select “maximize” for optimal viewing dimensions.

3. Use the arrow keys or the “page up” “page down” buttons to scroll through the left hemisphere until you find the first slice where the fimbria of the hippocampus has a detached appearance.  Image will be in radiological perspective. The space bar will change the picture in the main window.

4. Set crosshairs in the middle of the hippocampus, as shown by the red box in ROI 4 in the following slides. If crosshairs are not visible, go to “View” and select “main crosshairs”. 

5. Now that the crosshairs are in place we are ready to place the ROI. There is a separate small window that shows the coordinates of the crosshairs in the brain. This window automatically opens when Mango is running. In the small window there is a button with a red square on it. Clicking on this button will allow you to select the color of the ROI. The default is red which will be used for the left hemisphere. Green will be used for the right hemisphere.
 
6. Under the ROI tab in the top left corner, select “Add ROI”
 
7. Select “Cube”, width and radius should both be set to 2 mm. Then hit “OK” 

8. A red cube with set dimension should show up right in the middle of the hippocampus where your crosshairs were placed. This position can be adjusted by double clicking on it and dragging to desired location. An example is shown in the next slide.

9. Scroll laterally 3 slices, using the arrow keys or the “page up” “page down” buttons.

10. Place crosshairs on the posterior part of the hippocampus, and repeat steps 6-8. Be careful with your placements because if you now adjust position your previous ROI’s will move as well. ROI’s of the same color move as one.
 
11. On the same slice, place the crosshairs on the anterior part of the hippocampus and again repeat steps 6-8. You should have two red cubes on this one slice, as shown on the next slide.

12. Scroll laterally 3 slices, using the arrow keys or the “page up” “page down” buttons.

13. Place crosshairs in the middle of the hippocampus and repeat steps 6-8. It should look like image on next slide.

14. Scroll medially 6 slices to get to original slice. Scroll medially an additional 3 slices, again using the arrow keys or the “page up” “page down” buttons.

15. Place crosshairs on the posterior part of the hippocampus, and repeat steps 6-8.

16. On the same slice, place the crosshairs on the anterior part of the hippocampus and again repeat steps 6-8. You should again have two red cubes on this one slice as shown on the next slide.
You should now have all six ROIs placed as shown in slide 14 of attached powerpoint.

17. Double click on the ROIs 5 and 6 to highlight them. Under the “ROI” tab in the top left corner select “Dilate”. The setting is already preset to 3 so just hit “OK”.  This will dilate all your placed ROI of the same color.

18. Repeat above steps for the right hemisphere only change the ROI color to green. This can be done as mentioned in previous steps.
 
19. Save ROIs as a Nifti file by going to “File” and selecting “save ROI”. 
