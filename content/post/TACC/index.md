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
{{< gdocs src="https://docs.google.com/presentation/d/e/2PACX-1vQ5XM8CYAA18kBNhydN3aE9-OnR8BnDOI4gb7_lfOYV11RqKHrCpfTd5KIaRYSAUhSgJfmkS8LLxTde/embed?start=true&loop=true&delayms=15000" >}}

Example slurm file
```slurm
#!/bin/bash
#----------------------------------------------------
# Example SLURM job script to run code
#----------------------------------------------------
#SBATCH -J lab_job	 		# Job name
#SBATCH -o console_output.txt  		 # Name of stdout output file
#SBATCH -e console_error_output.txt   	# Name of stdout output error file
#SBATCH -p normal        			# Queue name
#SBATCH -N 1            			 # Total number of nodes requested, multi-node means parallel
#SBATCH -n 1             			# Total number of task requested
#SBATCH -t 01:30:00	 		# Run time (hh:mm:ss) - 1.5 hours, time you ask for, it will stop running after this time whether it’s finished or not
# The next line is required if the user has more than one project
#SBATCH -A XXXXl 		# Project/allocation number, the one you apply with
# This example will run 1 task on 1 nodes
# Launch the job, the file you want to run 
python ./file.py
```
