# Brain Image Processing Routines
*Updated 202512181231 by Josh Goh*

Currently, 
- This repository contains Bash and Matlab scripts for scaling brain image processing routines using control pipelines.
- Brain image preprocessing and statistical analysis routines are primarily configured to use SPM25.
- Bash shell scripts are configured for Ubuntu or CentOS Linux operating systems.

The usage mode is to pass Matlab routines in Bash shell script wrappers, and call these routines in Bash shell script pipelines. This allows for,
- Flexible control of routine order 
- Capacity to integrate routines based on other programming environments (e.g. Python, R).

## Dependencies
**1. MricroGL**
- This is needed for the dicom conversion tool (dcm2niix).
- This needs to be installed with dcm2niix (mricrogl; optional) in the system search path.
- Here is a sample script to install MricroGL in a manner that the pipelines here can use (as at 2026/12/18).
```
cd ~/Downloads
wget https://github.com/rordenlab/MRIcroGL/releases/download/v1.2.20220720/MRIcroGL_linux.zip
unzip MRIcroGL_linux.zip
sudo cp -rf MRIcroGL /opt/
cd /usr/local/bin
sudo ln -s /opt/MRIcroGL/MRIcroGL mricrogl
sudo ln -s /opt/MRIcroGL/Resources/dcm2niix dcm2niix
```

**2. Matlab**
- This should be downloaded from [MathWorks](https://www.mathworks.com) using your Mathworks account and installed as instructed on their website.
- The 'matlab' function then needs to be in the system search path.
- Here is a sample installation script after the installation zip file has been downloaded and unzipped (e.g. to the ~/Downloads/matlab_R2025b_Linux folder).
```
## Download Matlab installer (e.g. ver. R2025b) from mathworks.com (requires account), unzip
cd ~/Downloads/matlab_R2025b_Linux
xhost +SI:localuser:root
sudo -H ./install
xhost -SI:localuser:root 
cd /usr/local/bin
sudo ln -s /usr/local/MATLAB/2025b/bin/matlab
```

**3. SPM25**
- This should be installed and set up to be in the user-level Matlab's search path.
- Here is a sample installation script (as at 2026/12/18).
```
cd ~/Downloads
wget https://github.com/spm/spm/releases/download/25.01.02/spm_25.01.02.zip
unzip spm_25.01.02.zip
sudo cp -rf ~/Downloads/spm /opt/
echo "% SPM Setup" >> ~/Documents/MATLAB/startup.m
echo "addpath /opt/spm" >> ~/Documents/MATLAB/startup.m
echo "warning('off', 'MATLAB:class:LoadWarning');" >> ~/Documents/MATLAB/startup.m
```

**4. FSL**

**5. AFNI**

**6. Freesurfer**

*Note: For Brain and Mind Lab members, these are all already configured in our lab servers. See [Brain and Mind Lab's Setup Server Environment Gitlab](https://gitlab.com/brain-and-mind-lab/servers/setup-server-environment)*

## Installation 
**Ubuntu, CentOS (Linux)**
1. Download this repository to your local path (e.g. /home/user)
```
cd ~
wget https://github.com/joshuagohos/brain-processing-routines/archive/refs/heads/main.zip
```

2. Unzip the downloaded zip file.
```
unzip main.zip
```
This will results in a folder named brain-processing-routines. The folder contains the following:
```
brain-processing-routines
├── LICENSE
├── README.md
├── bin
├── pipelines
└── routines
```
- bin: symbolic links pointing to shell scripts in the routines directory. The contents in this folder should be copied to /usr/local/bin/
- pipelines: Control shell scripts that call routines scripts in the routine directory. These scripts should be placed in specific project code or script folders and modified for use accordingly.
- routines: Bash shell wrappers scripts passing brain processing functions into respective coding environments.

3. Copy the routines folder to /opt/brain-processing-routines/ and make executable.
```
sudo mkdir -p /opt/brain-processing-routines
sudo cp -rf brain-processing-routines/routines /opt/brain-processing-routines/
sudo chmod -R +x /opt/brain-processing-routines/routines/*
```

4. Make read/write/executable and copy the contents (symbolic links) of the bin folder to /usr/local/bin/.
```
sudo chmod +rwx brain-processing-routines/bin/*
sudo cp -rf brain-processing-routines/bin/* /usr/local/bin/
```

# Usage
Configure the pipeline scripts in brain-processing-routines/pipelines as needed and run. For example, after. configuring spm_pipeline.sh, run the following.
```
cd /path/to/project/brain-processing-routines/pipelines
./spm_pipelines.sh
```

