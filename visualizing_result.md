# Extract data from SPM clusters

```
cd ~/Desktop/spm-part-2/grp_covariate_age/
for var in $(find ~/Desktop/spm-part-2/ -type f -name "*.nii"); do
  c3d -verbose \
  $var \
  spmT_0001_cluster_0001.img \
  -label-statistics >> spmT_0001_cluster_0001.txt
done
```

# Reformat Text Output

Write a bash script with the following code and be sure to change <username> to the apporpriate computer username:

```bash
#!/bin/sh

filename="$1"

output="${filename%.*}_modified.csv"
cd $(dirname $filename)
string1="Reading #1 from /Users/njhunsak/Desktop/spm-part-2//smwrpGM_NORM_"
string2="Reading #1 from /Users/njhunsak/Desktop/spm-part-2//smwrpGM_TBI_"
string3=".nii"
grep -vwE "(Reading #2|LabelID|^(    0))" ${filename} > temp1.txt
sed \
  -e "s|$string1||" \
  -e "s|$string2||" \
  -e "s|$string3||" \
  -e "s|/|,|" \
  -Ee "s|[ ]+|,|g" temp1.txt > temp2.txt
awk '/^[0-9][0-9][0-9][0-9]/{print}' temp2.txt > part1.txt
awk '/^,/{print}' temp2.txt > part2.txt
paste part1.txt part2.txt > ${output}
perl -pi -e \
  'print "id, label, mean, std, max, min, count, volume, x, y, z\n" if($.==1)' \
  ${output}
rm part1.txt
rm part2.txt
rm temp*.txt
```

To run your new bash script type:

```
sh <nameofscript>.sh <txtfiletobemodified>.txt
```

# Import Demographic Data into R

Be sure you have the following packages installed. You only need to do this once on your computer:

```
install.packages(c("gdata","ggplot2"))
```

```
library(gdata)
setwd('~/Desktop/spm-part-2/')
demographic=read.xls('demographic.xls')
```

# Quick Plots in R

## Boxplot

Then you can graph your data:

```
library(ggplot2)
setwd('~/Desktop/spm-part-2/grp_covariate_age')
data=read.csv('spmT_0001_cluster_0001_modified.csv')
data=merge(data,demographic,by="ID",all.x=TRUE)
pdf('~/Desktop/spm-part-2/grp_covariate_age/spmT_0001_cluster_0001.pdf')
qplot(factor(Group),mean,data=data,geom=c("boxplot","jitter"),colour=Group,main="Norm > TBI Cluster 1")
dev.off()
```

```{r,echo=FALSE,tidy=TRUE,tidy.opts=list(width.cutoff=70)}
library(ggplot2)
setwd('~/Desktop/spm-part-2/grp_covariate_age')
data=read.csv('spmT_0001_cluster_0001_modified.csv')
data=merge(data,demographic,by="ID",all.x=TRUE)
qplot(factor(Group),mean,data=data,geom=c("boxplot","jitter"),colour=Group,main="Norm > TBI Cluster 1")
```

## Scatterplot
```
library(ggplot2)
setwd('~/Desktop/spm-part-2/correlation_fsiq')
data=read.csv('spmT_0001_cluster_0001_modified.csv')
data=merge(data,demographic,by="ID",all.x=TRUE)
pdf('~/Desktop/spm-part-2/correlation_fsiq/spmT_0001_cluster_0001.pdf')
qplot(WASIIQ,mean,data=data,main="WASI IQ+")+geom_smooth(method=lm,se=FALSE,fullrange=T)
dev.off()
```

```
library(ggplot2)
setwd('~/Desktop/spm-part-2/correlation_fsiq')
data=read.csv('spmT_0001_cluster_0001_modified.csv')
data=merge(data,demographic,by="ID",all.x=TRUE)
qplot(WASIIQ,mean,data=data,main="WASI IQ+")+geom_smooth(method=lm,se=FALSE,fullrange=T)
```

## Interaction
```
library(ggplot2)
setwd('~/Desktop/spm-part-2/interaction_fsiq')
data=read.csv('spmT_0003_cluster_0001_modified.csv')
data=merge(data,demographic,by="ID",all.x=TRUE)
pdf('~/Desktop/spm-part-2/interaction_fsiq/spmT_0003_cluster_0001.pdf')
qplot(WASIIQ,mean,data=data,main="Norm+ vs. TBI-",colour=Group)+geom_smooth(method=lm,se=FALSE,fullrange=T)
dev.off()
```

```
library(ggplot2)
setwd('~/Desktop/spm-part-2/interaction_fsiq')
data=read.csv('spmT_0003_cluster_0001_modified.csv')
data=merge(data,demographic,by="ID",all.x=TRUE)
qplot(WASIIQ,mean,data=data,main="Norm+ vs. TBI-",colour=Group)+geom_smooth(method=lm,se=FALSE,fullrange=T)
```