# NextBrain: a next-generation, histological atlas of the human brain for high-resolution neuroimaging studies.

> Official website: https://github-pages.ucl.ac.uk/NextBrain/#/home#pipeline

According to the [FreeSurfer document](https://surfer.nmr.mgh.harvard.edu/fswiki/HistoAtlasSegmentation) and [Next Brain Github](https://surfer.nmr.mgh.harvard.edu/fswiki/HistoAtlasSegmentation),
the simplified document to install and use:

## OS
Ubuntu 20.04

## Install 
Install Freesurfer 7.4.0 or newer.
```shell
# cd ./software
wget https://surfer.nmr.mgh.harvard.edu/pub/dist/freesurfer/7.4.1/freesurfer-linux-ubuntu20_amd64-7.4.1.tar.gz
tar -xzvf ./freesurfer-linux-ubuntu20_amd64-7.4.1.tar.gz
# rm -rf ./freesurfer-linux-ubuntu20_amd64-7.4.1.tar.gz

# add freesurfer path to your home ~/.bashrc
export FREESURFER_HOME=/your_path/software/freesurfer
source $FREESURFER_HOME/SetUpFreeSurfer.sh

# download the segmentation code to fold with any name (like: segmentation)
# https://github.com/freesurfer/freesurfer/tree/dev/mri_histo_util

# download the atlas
cd ./segmentation_code/ERC_bayesian_segmentation
wget https://ftp.nmr.mgh.harvard.edu/pub/dist/lcnpublic/dist/Histo_Atlas_Iglesias_2023/atlas_full.zip
unzip ./atlas_full.zip
rm ./atlas_full.zip
mv ./ERC_bayesian_segmentation/* ../freesurfer/python/packages/ERC_bayesian_segmentation/
```

## Usage

```shell
cd ./segmentation_code

./mri_histo_atlas_segment.sh INPUT_SCAN OUTPUT_DIRECTORY ATLAS_MODE GPU THREADS [BF_MODE] [GMM_MODE]

INPUT SCAN: scan to process, in nii(.gz) or mgz format
OUTPUT_DIRECTORY: directory where segmentations, volume files, etc will be written (more on this below).
ATLAS_MODE: must be full (all 333 labels) or simplified (simpler brainstem protocol; recommended)
GPU: set to 1 to use the GPU (highly recommended but requires a 24GB GPU!)
THREADS: number of CPU threads to use (use -1 for all available threads)
BF_MODE (optional): bias field mode: dct (default), polynomial, or hybrid
GMM_MODE (optional): gaussian mixture model (GMM) model must be 1mm unless you define your own (see documentation)

# for example
./mri_histo_atlas_segment /your_path/HCP/100307/T1w/T1w_acpc_dc_restore_brain.nii.gz /your_path/atlas_testbench/100307 full 1 -1
```

## Time consumption

For one subject in HCP, 1 hour on GPU, 1.5 days on CPU.


