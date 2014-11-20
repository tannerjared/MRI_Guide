Statistical Parametric Mapping (SPM) software is a suite of MATLAB. The latest version is SPM12 released October 1st, 2014, but we will use the previous version SPM8, because there's a useful toolbox VBM8 for VBM analyses.

# Download and Install SPM

You can download the latest version from: http://www.fil.ion.ucl.ac.uk/spm/software/download.html. After the zip file has downloaded, copy the spm8 directory to your MATLAB directory. In your terminal window:

```bash
mkdir ~/MATLAB/spm8
cp -r ~/Downloads/spm8/ ~/MATLAB/spm8
```

Everytime MATLAB opens, you will want to make sure it loads the SPM folder, much like setting the environmental variables for ANTs and FSL, we need to set the variables for MATLAB. We do this by creating a new script that will run at startup. Select `Command N` or go to File > New > Script. Add this text into your new script:

```matlab
SPM8Path = '/<Path>/<to>/MATLAB/spm8';
addpath(genpath(SPM8Path));
fprintf('Adding %s\n', SPM8Path);
```

Save this file as `startup.m` within your MATLAB directory.

# Download and Install VBM8 Toolbox

The VBM8 Toolbox runs the basic steps of SPM VBM analyses, but provides some useful extensions. You can download the latest version from: http://dbm.neuro.uni-jena.de/vbm8/. Copy and paste the file into your spm8 toolbox directory:

```bash
mkdir ~/MATLAB/spm8/toolbox/vbm8
cp -r ~/Downloads/vbm8/ ~/MATLAB/spm8/toolbox/vbm8
```