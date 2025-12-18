# Brain Processing Routines
*Updated 202512181231 by Josh Goh*

Currently, 
- This repository contains Bash and Matlab scripts for scaling brain image processing routines using control pipelines.
- Brain image preprocessing and statistical analysis routines are primarily configured to use SPM25.
- Bash shell scripts are configured for Ubuntu or CentOS Linux operating systems.

The usage mode is to pass Matlab routines in Bash shell script wrappers, and call these routines in Bash shell script pipelines. This allows for,
- Flexible control of routine order 
- Capacity to integrate routines based on other programming environments (e.g. Python, R).

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

3. Copy routines to /opt and make executable.
```
sudo cp -rf brain-processing-routines/routines /opt/
sudo chmod -R +x /opt/routines/*
```
