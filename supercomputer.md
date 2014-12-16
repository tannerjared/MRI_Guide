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

[Reading Materials and Lecture Slides](manuals_slides)

---------------------------------------

# How to Logon the FSL Supercomputer

```bash
ssh <netid>@ssh.fsl.byu.edu
```

# Install Programs

You will have to create you own apps directory under your home directory:

```bash
mkdir bin
cd bin
```

## Advanced Normalization Tools

Under your bin directory, download the latest version of ANTs:

```bash
git clone git://github.com/stnava/ANTs.git
```

Install ANTs:

```
module load cmake/2.8.10.2
mkdir antsbin
cd antsbin
ccmake ../ANTs
```

Configure ANTs by pressing the "c" key. Continue pressing the "c" key until no new options appear. When no new otpions appear in CMake, you can proceed to generate Makefiles by hitting the "g" key. Once you are back at your regular terminal prompt:

```
make -j 4
```
You will also need to copy all of the scripts into your `antsbin/bin` folder

```
cp /fslhome/<netid>/bin/Ants/Scripts/* /fslhome/<netid>/bin/antsbin/bin/

````

and wait awhile. Your ANTSPATH will be slightly different and needs to be included in ALL scripts:


```
export ANTSPATH=/fslhome/<netid>/bin/antsbin/bin/
PATH=${ANTSPATH}:${PATH}
```

## ITK

Under your bin directory, download the latest version of ITK:

```bash
cd ~/bin
git clone git://itk.org/ITK.git
```

Install ITK:

```bash
mkdir ITK-build
cd ITK-build
ccmake ../ITK
```

Configure ITK by pressing the "c" key. In order to speed up the build process, disable the compliation of the unit tests and examples. This is done with the variables `BUILD TESTING=OFF` and `BUILD EXAMPLES=OFF`. Each time you change a set of variables in CMake, it is necessary to proceed to another configuration step by hitting the "c" key. When no new options appear in CMake, you cna proceed to generate Makefiles by hitting the "g" key.

```bash
make
```

## SegAdapter

Under your bin directory, download the latest version of SegAdpater:

```bash
cd ~/bin
wget http://www.nitrc.org/frs/download.php/5859/segAdapter_1.9_release.tar.gz
tar -xzvf segAdapter_1.9.tar.gz
cd segAdapter_1.9_release/
```

You will need to edit the CMakeList.txt file:

```bash
vi CMakeLists.txt
```

To edit the text, press the "a" key. You will need to change the following:

> TARGET_LINK_LIBRARIES(sa ITKNumerics ITKIO ITKStatistics)    
> TARGET_LINK_LIBRARIES(bl ITKNumerics ITKIO ITKStatistics)

to the correct ITK libraries:

> TARGET_LINK_LIBRARIES(sa ${ITK_LIBRARIES})    
> TARGET_LINK_LIBRARIES(bl ${ITK_LIBRARIES})

When you are done editing your file, press the "esc" key. To save the file, press ":wq" and then enter.


Install SegAdapter:

```bash
ccmake .
```

Configure SegAdapter by pressing the "c" key. You need to change the variable `ITK_DIR` to /fslhome/<netid>bin/ITK-build/`. Each time you change a set of variables in CMake, it is necessary to proceed to another configure setp by hitting the "c" key. When no new options appear in CMake, you can proceed to generate Makefiles by hitting the "g" key.

```bash
make
```

You will need to provide the full pathname when you want to run SegAdapter:

```bash
/fslhome/<netid>/bin/segAdapter_1.9_release/bl
/fslhome/<netid>/bin/segAdapter_1.9_release/sa
```

## acpcdetect

Under your bin directory, download the latest version of acpcdetect:

```bash
cd ~/bin
mkdir art
cd art
wget http://www.nitrc.org/frs/download.php/6494/acpcdetect.tar.gz
tar -xvzf acpcdetect.tar.gz
```

You need to set your $ARTHOME environment variable in all scripts:

```bash
ARTHOME=/fslhome/<netid>/bin/art
export ARTHOME
```

# rsync Data from Local Drive to Supercomputer

Log out of your FSL account if you haven't already:

```bash
exit
```

To sync from your local computer to the supercomputer, use rsync. You can first *verify* the files that are going to sync over using the `--dry-run` option.

```bash
rsync -rauv --exclude=".*" -e ssh ~/Desktop/supercomputer/ \
<netid>@ssh.fsl.byu.edu:~/compute --dry-run
```

If you are comfortable with the files to be synced:

```bash
rsync -rauv --exclude=".*" -e ssh ~/Desktop/supercomputer/ \
<netid>@ssh.fsl.byu.edu:~/compute
```

# Script to run single participant

Log onto the supercomputer and then create a folder for your logfiles:

```bash
ssh <netid>@ssh.fsl.byu.edu
timestamp=$(date '+%Y_%m_%d_%H%M')
mkdir -p logfiles/${timestamp}
```

Create a folder for your scripts:

```bash
cd
mkdir -p scripts/acpcdetect
```

Generate a new script:

```bash
cd scripts/acpcdetect/
vi do_acpcdetect0.sh
```

Edit the following text. Press the "a" key to insert text into your new file. Copy and paste into your new script:

```bash
#!/bin/bash

#SBATCH --time=50:00:00   # walltime
#SBATCH --ntasks=1   # number of processor cores (i.e. tasks)
#SBATCH --nodes=1   # number of nodes
#SBATCH --mem-per-cpu=8192M   # memory per CPU core
#SBATCH -o /fslhome/<netid>/logfiles/YYYY_MM_DD_HHMM/output_acpcdetect0.txt
#SBATCH -e /fslhome/<netid>/logfiles/YYYY_MM_DD_HHMM/error_acpcdetect0.txt
#SBATCH -J "acpcdetect0"   # job name
#SBATCH --mail-user=   # email address
#SBATCH --mail-type=BEGIN
#SBATCH --mail-type=END
#SBATCH --mail-type=FAIL

# Compatibility variables for PBS. Delete if not needed.
export PBS_NODEFILE=`/fslapps/fslutils/generate_pbs_nodefile`
export PBS_JOBID=$SLURM_JOB_ID
export PBS_O_WORKDIR="$SLURM_SUBMIT_DIR"
export PBS_QUEUE=batch

# Set the max number of threads to use for programs using OpenMP.
export OMP_NUM_THREADS=$SLURM_CPUS_ON_NODE

# LOAD MODULES, INSERT CODE, AND RUN YOUR PROGRAMS HERE
export ARTHOME=/fslhome/<netid>/bin/art

IFS=$'\n'
array=( $(find ~/compute/practice/ -type f -name "t1.nii") )
for i in 0; do
  subjDir=$(dirname ${array[$i]})
	~/bin/art/acpcdetect -M -o ${subjDir}/acpc.nii -i ${array[$i]}
done
```

In order to generate a script for each of your participants, you must determine the number of files to be processed:

```bash
IFS=$'\n'
array=( $(find ~/compute/practice/ -type f -name "t1.nii") )
echo ${#array[@]}
```

To generate the files for each participant:

```bash
cd ~/scripts/acpcdetect/
max=$((${#array[@]}-2))
for i in $(seq 0 $max); do
    num=$i
    new=$(($num+1))
    sed \
    -e 7s/acpcdetect$num/acpcdetect$new/g \
    -e 8s/acpcdetect$num/acpcdetect$new/g \
    -e 9s/acpcdetect$num/acpcdetect$new/g \
    -e 29s/$num/$new/g \
    do_acpcdetect$num.sh > do_acpcdetect$new.sh
done
```

To generate a script to submit each participant script:

```bash
cd ~/scripts
max=$((${#array[@]}-1))
for i in $(seq 0 $max); do
    echo "sbatch ~/scripts/acpcdetect/do_acpcdetect$i.sh ;" \
    >> run_acpcdetect_${timestamp}.sh
done
```


When you are ready to submit your jobs:

```bash
sh run_acpcdetect_${timestamp}.sh
```

You can check up on your job status several ways:

1. If you set up your email, you should receive an email when the job begins, ends, or aborts.
2. You can type in `squeue -u <netid>` to see the status.
3. You can read the output and error files, `cat ~/logfiles/${timestamp}/output_acpcdetect0.txt`

# rsync Data from Supercomputer to Local Drive

Make sure you are not logged onto the super computer first. To sync from the supercomputer to your local computer, use rsync. You can *verify* the files that are going to sync over using the `--dry-run` option.

```bash
rsync -rauv --exclude=".*" -e ssh <netid>@ssh.fsl.byu.edu:~/compute/practice/ \
~/Desktop/supercomputer/practice --dry-run
```

If you are comfortable with the files to be synced:

```bash
rsync -rauv --exclude=".*" -e ssh <netid>@ssh.fsl.byu.edu:~/compute/practice/ \
~/Desktop/supercomputer/practice
```
