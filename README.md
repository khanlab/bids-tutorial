# bids-tutorial
Resources for tutorial on BIDS - Methods Lunch Feb 12


##  Materials:
https://github.com/INCF/bids-starter-kit/wiki


## Tutorial agenda
1. What is BIDS
2. Creating a BIDS dataset
3. BIDS Apps




## What is BIDS

* Overall structure
* NIFTI vs BIDS?
* JSON
* TSV
* Other principles: Inheritance, ...

http://bids.neuroimaging.io/

## Creating a BIDS dataset

* Curation by hand
* bids-validator (web-based, command-line)
* dcm2niix (json support)
* Hands-on demo 

http://incf.github.io/bids-validator/

## The cfmm-bids tool 

* Heuristic-based conversion with heudiconv
* Dicom server retrieval
* Dicom file grabbing
* Hands-on demo (requires Linux with Singularity for audience)


## BIDS Apps

* Overall structure (in, out, participant level)
* Flexibility --> any programming language!
* Containers
* Docker vs Singularity
* Existing BIDS-Apps
  * fmriprep
  * mriqc
  * in-house apps 
* Hands-on demo (use pre-built Singularity image)

http://bids-apps.neuroimaging.io/apps/

Containers:
https://www.docker.com/
http://singularity.lbl.gov/
https://www.singularity-hub.org/

## Compute Canada & KhanLab/autobids - next time!

## Appendix:

### Installing Singularity:
```
VERSION=2.4.2
wget https://github.com/singularityware/singularity/releases/download/$VERSION/singularity-$VERSION.tar.gz
tar xvf singularity-$VERSION.tar.gz
cd singularity-$VERSION
./configure --prefix=/usr/local
make
sudo make install
sudo apt-get install -y squashfs-tools
```

### Getting the cfmm-bids Singularity app

# under construction -- going to revert back to 3 separate singularity tools (and mainly go over tar2bids in the tutorial)

The cfmm-bids singularity app actually contains 3 separate tools that can be run from the command-line.

To download cfmm-bids:
```
mkdir ~/bids-tutorial
cd ~/bids-tutorial
singularity pull shub://khanlab/cfmm-bids:v0.0.3
``` 

List apps in cfmm-bids:
```
singularity apps khanlab-cfmm-bids-master-v0.0.3.simg 
```

Should see that three apps are listed: cfmm2tar, dicom2tar, tar2bids
You can run these apps with `singularity run -app <name>`:

Run tar2bids:
```
singularity run -app tar2bids khanlab-cfmm-bids-master-v0.0.3.simg
```

You should see the usage for tar2bids now:
```
Runs dicom tarball(s) to BIDS conversion using heudiconv
Usage: tar2bids  <optional flags>  '<{subject} search string>'  <in tar file(s)>

 Optional flags (must appear before required arguments):
	-o <output_dir> : default=./bids
	-N <num parallel cores> : default=0  (max cores)
	-h <heuristic.py> : default=cfmm_bold_rest.py
	-O "<additional heudiconv options>" : default=

 Available heuristic files:
	EPL14A_GE_3T.py
	EPL14B_3T.py
	GEvSE.py
	cfmm_PS_PRC_3T.py
	cfmm_base.py
	cfmm_bold_rest.py
```




Links:
* https://github.com/khanlab/cfmm-bids
* https://www.singularity-hub.org/collections/585
