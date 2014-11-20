# Other ways to acquire Dice's Coefficient and Label Statistics

Instead of using convert3d or FSL you can also use ANTs, to generate a file per participant. Unsure if you can output to the same file for an entire study. You could always merge files with the following command:

```
cat *.txt > merged.txt
```

```
# Dice's Coefficient in c3d
c3d -verbose <LabelImage1>.nii.gz <LabelImage2>.nii.gz -overlap <labelValue>

# Label Statistics in c3d
c3d <t1wImage>.nii.gz <LabelImage>.nii.gz -label-statistics

# Dice's Coefficient in ANTs
ImageMath 3 <outputPrefix> DiceAndMinDistSum <LabelImage1>.nii.gz <LabelImage2>.nii.gz

# Label Statistics in ANTs
ImageMath 3 <outputPrefix> LabelStats <LabelImage>.nii.gz

# Label Statistics in FSL
fslstats <LabelImage>.nii.gz -l <1-labelValue> -u <1+labelValue> -V
```

You can use these different ways as a sanity check if you are unsure what data is being generated.