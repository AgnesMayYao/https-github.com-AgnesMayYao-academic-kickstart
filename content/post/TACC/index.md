+++
title = "How to use supercomputers from Texas Advanced Computing Center (TACC)"
subtitle = "Boost your training speed"

date = 2019-10-01T00:00:00
lastmod = 2019-10-01T00:00:00
draft = false

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["admin"]

tags = ["TACC"]
summary = "use TACC to run code / train model"

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["deep-learning"]` references 
#   `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
# projects = ["internal-project"]

# Featured image
# To use, add an image named `featured.jpg/png` to your project's folder. 
[image]
  # Caption (optional)
  # caption = "Image credit: [**Unsplash**](https://unsplash.com/photos/CpkOjOcXdUY)"

  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = ""

  # Show image only in page previews?
  preview_only = false

# Set captions for image gallery.


+++
## Before you begin
1. Create a TACC account (https://portal.tacc.utexas.edu/)
2. Solve Multi-factor authentication at TACC user portal
  * different from utexas multi-factor authentication
  * https://portal.tacc.utexas.edu/tutorials/multifactor-authentication

## Login
1. ```shell
    ssh xy0000@hikari.tacc.utexas.edu
   ```
  * Replace xy0000 with your own eid
  * Replace hikari with your own system (eg. maverick2, lonestar5) 
2. Login using your TACC password and multi-factor authentication token code

## Transfer file
```shell
  # For file
  localhost$ scp path/to/file xy0000@maverick2.tacc.utexas.edu:\$WORK/path
  # For folder
  localhost$ tar cvf ./mydata.tar mydata                                   # create archive
  localhost$ scp     ./mydata.tar xy0000@maverick2.tacc.utexas.edu:\$WORK  # transfer archive
```
  * **WORK** directory is usually larger than **HOME** directory
  
## Run
### Method 1 (sbatch)
1. Do not run the code directly at login.
2. Create a .slurm file
  * Example slurm file below:
```slurm
#!/bin/bash
#----------------------------------------------------
# Example SLURM job script to run code
#----------------------------------------------------
#SBATCH -J lab_job	 		                # Job name
#SBATCH -o console_output.txt  		      # Name of stdout output file
#SBATCH -e console_error_output.txt   	# Name of stdout output error file
#SBATCH -p normal        			          # Queue name
#SBATCH -N 1            			          # Total number of nodes requested, multi-node means parallel
#SBATCH -n 1             			          # Total number of task requested
#SBATCH -t 01:30:00	 		                # Run time (hh:mm:ss) your allocation ends in 1.5 h (program can be unfinished)
# The next line is required if the user has more than one project
#SBATCH -A XXXX 		                    # Project/allocation number, the one you apply to TACC with
# This example will run 1 task on 1 nodes
# Launch the job, the file you want to run 
python ./file.py
```
3. Run slurm
```shell
  login2.hikari(26)$ sbatch your_filename.slurm
```
4. Watch the job
  * 
  ```shell
  login2.hikari(41)$ watch squeue
  login2.hikari(29)$ squeue
       JOBID   PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
       47767      normal  lab_job   xy0000  R       0:06      1 c262-102
  ```
5. Check console output
  ```shell
  cat console_output.txt 
  ```
  * the file you define in slurm
6. Cancel job
  ```shell
  login2.hikari(41)$ scancel 47767 
  ```
  * scancel JOBID
    
## Run
### Method 2 (idev)
1. 
  ```shell
  login2.hikari(36)$ idev -t 01:30:00 
  ```
  * idev: interactive development something
  * -t the total time you requested
  * This one doesn’t need slurm file 
2. 
  ```shell
  c262-104.hikari(2)$ python file.py 
  ```
  * Run the code as normal like in a terminal, same speed as the one with slurm
3. 
  ```shell
  c262-104.hikari(3)$ squeue
             JOBID   PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
           47769      normal idv08693   xy0000  R       3:20      1 c262-104
  ```
4. Logout
  ```shell
  c262-104.hikari(4)$ exit
  Connection to c262-104 closed.
  Cleaning up: submitted job (yes) removing job 47769.
  ```
  
## Deep Learning Using Python
1. Use Python 3 if you need h5py
2. Input following before running your code
```shell
  module load intel/17.0.4 python3/3.6.3
  module load cuda/10.0 cudnn/7.6.2 nccl/2.4.7
  pip3 install --user tensorflow-gpu==1.13.2
  pip3 install --user keras
  pip3 install --user h5py
```



