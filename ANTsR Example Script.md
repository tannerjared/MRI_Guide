```
library(ANTsR)
setwd("/fslhome/zach8769/compute/rsobik/WASIMatrixReasoning/")
load("/fslhome/zach8769/compute/rsobik/WASIMatrixReasoning/vardata")
load("/fslhome/zach8769/compute/rsobik/WASIMatrixReasoning/varmat")
mask<-getMask(antsImageRead("/fslhome/zach8769/compute/7_13_template/brainmask.nii.gz"))
#prepare contrasts
ig<-vardata$InjuryGroup
ig<-factor(ig,levels=c("oi","mild","mod","sev"))
conmat=matrix(c(1/4,1/4,1/4,1/4,1,-1,0,0,1,0,-1,0,1,0,0,-1),ncol=4)
mymat=solve(t(conmat))
my.contrasts<-mymat[,2:4]
contrasts(ig)=my.contrasts

#variable
var1<-vardata[,10]

bynum<-1
ss<-seq(1,ncol(varmat),by=bynum)

#matrices for pvalues
pval.oi.v.mild<-rep(1,ncol(varmat))
pval.oi.v.mod<-rep(1,ncol(varmat))
pval.oi.v.sev<-rep(1,ncol(varmat))

#matrices for tstat
tstat.oi.v.mild<-rep(1,ncol(varmat))
tstat.oi.v.mod<-rep(1,ncol(varmat))
tstat.oi.v.sev<-rep(1,ncol(varmat))

#matrices for coefficients
coef.oi.v.mild<-rep(1,ncol(varmat))
coef.oi.v.mod<-rep(1,ncol(varmat))
coef.oi.v.sev<-rep(1,ncol(varmat))

#each iteration performs the test on one column of the image matrix
for (i in ss)
{
vox<-varmat[,i]
fit<-lm(vox~var1+ig)
sumfit<-summary(fit)
#extract pvalues
pval.oi.v.mild[i]<-sumfit$coefficients[3,4]
pval.oi.v.mod[i]<-sumfit$coefficients[4,4]
pval.oi.v.sev[i]<-sumfit$coefficients[5,4]

#extract tstat
tstat.oi.v.mild[i]<-sumfit$coefficients[3,3]
tstat.oi.v.mod[i]<-sumfit$coefficients[4,3]
tstat.oi.v.sev[i]<-sumfit$coefficients[5,3]
}
save(object=pval.oi.v.mild,file="/fslhome/zach8769/compute/rsobik/WASIMatrixReasoning/pval.oi.v.mild")
save(object=pval.oi.v.mod,file="/fslhome/zach8769/compute/rsobik/WASIMatrixReasoning/pval.oi.v.mod")
save(object=pval.oi.v.sev,file="/fslhome/zach8769/compute/rsobik/WASIMatrixReasoning/pval.oi.v.sev")

save(object=tstat.oi.v.mild,file="/fslhome/zach8769/compute/rsobik/WASIMatrixReasoning/tstat.oi.v.mild")
save(object=tstat.oi.v.mod,file="/fslhome/zach8769/compute/rsobik/WASIMatrixReasoning/tstat.oi.v.mod")
save(object=tstat.oi.v.sev,file="/fslhome/zach8769/compute/rsobik/WASIMatrixReasoning/tstat.oi.v.sev")

##Export pvalue images
#OI vs Mild
pval.oi.v.mild<-matrix(pval.oi.v.mild, nrow=1)
pval.oi.v.mild<-p.adjust(pval.oi.v.mild,method="BH")
i.pval.oi.v.mild<-makeImage(mask,pval.oi.v.mild)
antsImageWrite(i.pval.oi.v.mild,file="/fslhome/zach8769/compute/rsobik/WASIMatrixReasoning/pval_oivmild.nii.gz")
#OI vs Moderate
pval.oi.v.mod<-matrix(pval.oi.v.mod, nrow=1)
pval.oi.v.mod<-p.adjust(pval.oi.v.mod,method="BH")
i.pval.oi.v.mod<-makeImage(mask,pval.oi.v.mod)
antsImageWrite(i.pval.oi.v.mod,file="/fslhome/zach8769/compute/rsobik/WASIMatrixReasoning/pval_oivmod.nii.gz")
#OI vs Severe
pval.oi.v.sev<-matrix(pval.oi.v.sev, nrow=1)
pval.oi.v.sev<-p.adjust(pval.oi.v.sev,method="BH")
i.pval.oi.v.sev<-makeImage(mask,pval.oi.v.sev)
antsImageWrite(i.pval.oi.v.sev,file="/fslhome/zach8769/compute/rsobik/WASIMatrixReasoning/pval_oivsev.nii.gz")

##Export tstat images
#OI vs Mild
tstat.oi.v.sev<-matrix(tstat.oi.v.sev, nrow=1)
i.tstat.oi.v.mild<-makeImage(mask,tstat.oi.v.mild)
antsImageWrite(i.tstat.oi.v.mild,file="/fslhome/zach8769/compute/rsobik/WASIMatrixReasoning/tstat_oivmild.nii.gz")
#OI vs Moderate
tstat.oi.v.sev<-matrix(tstat.oi.v.sev, nrow=1)
i.tstat.oi.v.mod<-makeImage(mask,tstat.oi.v.mod)
antsImageWrite(i.tstat.oi.v.mod,file="/fslhome/zach8769/compute/rsobik/WASIMatrixReasoning/tstat_oivmod.nii.gz")
#OI vs Severe
tstat.oi.v.sev<-matrix(tstat.oi.v.sev, nrow=1)
i.tstat.oi.v.sev<-makeImage(mask,tstat.oi.v.sev)
antsImageWrite(i.tstat.oi.v.sev,file="/fslhome/zach8769/compute/rsobik/WASIMatrixReasoning/tstat_oivsev.nii.gz")

##Export pval image including only values between 0 and .05 and binarized
#OI vs Mild
thresh.pval.oi.v.mild<-thresholdImage(i.pval.oi.v.mild,0,.05,inval=1,outval=0)
thresh.pval.oi.v.mild<-maskImage(thresh.pval.oi.v.mild,mask)##I might not need these last two if the first one works
thresh.pval.oi.v.mild<-labelClusters(thresh.pval.oi.v.mild,150,0,0.05)
antsImageWrite(thresh.pval.oi.v.mild,file="/fslhome/zach8769/compute/rsobik/WASIMatrixReasoning/pval_oivmild_thresh.nii.gz")
#OI vs Moderatela
thresh.pval.oi.v.mod<-thresholdImage(i.pval.oi.v.mod,0,.05,inval=1,outval=0)
thresh.pval.oi.v.mod<-maskImage(i.pval.oi.v.mod,mask)##I might not need these last two if the first one works
thresh.pval.oi.v.mod<-labelClusters(thresh.pval.oi.v.mod,150,0,0.05)
antsImageWrite(thresh.pval.oi.v.mod,file="/fslhome/zach8769/compute/rsobik/WASIMatrixReasoning/pval_oivmod_thresh.nii.gz")
#OI vs Severe
thresh.pval.oi.v.sev<-thresholdImage(i.pval.oi.v.sev,0,.05,inval=1,outval=0)
thresh.pval.oi.v.sev<-maskImage(thresh.pval.oi.v.sev,mask)##I might not need these last two if the first one works
thresh.pval.oi.v.sev<-labelClusters(thresh.pval.oi.v.sev,150,0,0.05)
antsImageWrite(thresh.pval.oi.v.sev,file="/fslhome/zach8769/compute/rsobik/WASIMatrixReasoning/pval_oivsev_thresh.nii.gz")

##Export info about each cluster
#OI vs Mild
#labels.oi.v.mild<-labelImageCentroids(thresh.pval.oi.v.mild)
pvaldata.oi.v.mild<-labelGeometryMeasures(thresh.pval.oi.v.mild)
write.csv(pvaldata.oi.v.mild,file="/fslhome/zach8769/compute/rsobik/WASIMatrixReasoning/oi_mild.csv")

#OI vs Moderate
#labels.oi.v.mod<-labelImageCentroids(thresh.pval.oi.v.mod)
pvaldata.oi.v.mod<-labelGeometryMeasures(thresh.pval.oi.v.mod)
write.csv(pvaldata.oi.v.mod,file="/fslhome/zach8769/compute/rsobik/WASIMatrixReasoning/oi_mod.csv")
#OI vs Severe
#labels.oi.v.sev<-labelImageCentroids(thresh.pval.oi.v.sev)
pvaldata.oi.v.sev<-labelGeometryMeasures(thresh.pval.oi.v.sev)
write.csv(pvaldata.oi.v.sev,file="/fslhome/zach8769/compute/rsobik/WASIMatrixReasoning/oi_sev.csv")
```
