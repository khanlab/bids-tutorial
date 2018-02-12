# bids-tutorial
Resources for tutorial on BIDS - Methods Lunch Feb 12


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

1. http://bids.neuroimaging.io/
2. https://github.com/INCF/bids-starter-kit/wiki
3. https://github.com/INCF/BIDS-examples
4.  http://jsoneditoronline.org

## Creating a BIDS dataset

* Curation by hand
* bids-validator (web-based, command-line)
* dcm2niix (json support)
* Hands-on demo 

1. http://incf.github.io/bids-validator/
2. https://www.nitrc.org/projects/dcm2nii/
3. http://www.mathworks.com/matlabcentral/fileexchange/42997


## BIDS Apps

* Overall structure (input, output, analysis_level)
* Flexibility --> any programming language!
* Containers
* Docker vs Singularity
* Existing BIDS-Apps
  * fmriprep
  * mriqc
  * in-house apps 
* Hands-on demo


Links
1. http://bids-apps.neuroimaging.io/apps/
2. https://www.docker.com/
3. http://singularity.lbl.gov/
4. https://www.singularity-hub.org/

### Running bids-app with Singularity:

Download and create a singularity image from docker hub:
```
sudo singularity pull docker://poldracklab/fmriprep:1.0.6
```

To run it:
```
singularity run fmriprep-1.0.6.simg
```
 

## The cfmm-bids tool 

* Heuristic-based conversion with heudiconv
* Dicom server retrieval
* Dicom file grabbing
* Hands-on demo


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

### Automated bids conversion with tar2bids

Download the cfmm-bids suite:
```
singularity pull shub://khanlab/tar2bids
singularity pull shub://khanlab/cfmm2tar
singularity pull shub://khanlab/dicom2tar
```

Run tar2bids:
```
singularity run khanlab-tar2bids-master-latest.simg
```

You should see the usage for tar2bids:
```
Runs dicom tarball(s) to BIDS conversion using heudiconv
Usage /opt/tar2bids/tar2bids  <optional flags>   <in tar file(s)>

 Optional flags (must appear before required arguments):
	-P <patient name search string> :  default:  *_{subject}
	-T <tar name search string> :  uses tarfile name instead of PatientName to search, e.g. '{subject}' if <subject>.tar
	-o <output_dir> : default=./bids
	-N <num parallel cores> : default=0  (max cores)
	-h <heuristic.py> : default=cfmm_bold_rest.py
	-O "<additional heudiconv options>" : default=

 Available heuristic files:
	cfmm_base.py
	cfmm_bold_rest.py
	cfmm_PS_PRC_3T.py
	EPL14A_GE_3T.py
	EPL14B_3T.py
	GEvSE.py
```

Links:
* https://github.com/khanlab/cfmm-bids
* https://github.com/nipy/heudiconv
* https://github.com/khanlab/heudiconv (cfmm-specific changes..)
* https://www.singularity-hub.org/collections/585
* http://nipy.org/workshops/2017-03-boston/lectures/bids-heudiconv/#1
