# Preprocessing

Before preprocessing, make sure all of your data is downloaded and in the appropriate directory.

## Gathering and organizing data

### Downloading your data

You will download your data from NIDB under Lepley-ACLr. The data will look like this:

*insert image of NIDB here*

For analyzing the functional data, the important files will be named _______.

To download the data from NIDB, use these options:
 
* Download Type > Destination: Web
* Data: Imaging, Behavioral, QC
* Format: DICOM, No DICOM anonymization, Gzip files
* Directory Structure > Directory Format: Primary alternate subject ID
* Directory Structure > Series Directories: Renumber series

### Storing your data

Once you have downloaded the data, be sure to have the data stored in BIDS format. For example:

`./Desktop/ACLr/sub-**/func/`
`./Desktop/ACLr/sub-**/anat/`
`./Desktop/ACLr/sub-**/misc/`

Structuring your file system in BIDS format can be done by hand, or there are automated scripts for doing this, e.g. <https://github.com/jmtyszka/bidskit>

If you are organizing the data by hand, you will need to use the `dcm2nii` function we downloaded. Code for performing this function might look like this:

`dcm2nii -a y -b y -g y -n y ./Desktop/sub-01/func/`

where the final subdirectory specified is the one in which your raw DICOM files are located.

First, you will need your timing files. These will tell us when participants were instructed to either rest or move their legs, and we are using a fixed timing file. The timing files should be stored in the `/misc/` directory of your BIDS file structure.

Your T1 structural files will go in the `/anat/` subdirectory, and your BOLD files will go in the `/func/` subdirectory.

## Generating preprocessing scripts

In this step, we will generate the preprocessing scripts you will need to actually preprocess your data. The scripts were originally made using uber_subject.py from AFNI and then modified by me. These scripts will generate preprocessing scripts and put them in each subject's folder.


