# HCP-MMP1.0: volumetric (NIfTI) masks in native structural space
> Official website: https://cjneurolab.org/2016/11/22/hcp-mmp1-0-volumetric-nifti-masks-in-native-structural-space/

According to the [FreeSurfer document](https://surfer.nmr.mgh.harvard.edu/fswiki/HistoAtlasSegmentation), [HCP-MMP 1.0 official page](https://cjneurolab.org/2016/11/22/hcp-mmp1-0-volumetric-nifti-masks-in-native-structural-space/) and a [github repo](https://github.com/tannerjared/HCP-MMP1) that converts the Connectome Workbench files to volume masks in native structural space and generates look up tables,
the simplified document to install and use:

## OS
Ubuntu 20.04

## Usage
Install Freesurfer 7.4.0 or newer.
```shell
# cd ./software
wget https://surfer.nmr.mgh.harvard.edu/pub/dist/freesurfer/7.4.1/freesurfer-linux-ubuntu20_amd64-7.4.1.tar.gz
tar -xzvf ./freesurfer-linux-ubuntu20_amd64-7.4.1.tar.gz
# rm -rf ./freesurfer-linux-ubuntu20_amd64-7.4.1.tar.gz

# add freesurfer path to your home ~/.bashrc
export FREESURFER_HOME=/your_path/software/freesurfer
source $FREESURFER_HOME/SetUpFreeSurfer.sh
```

Create a SUBJECTS_DIR folder and add it to your home ~/.bashrc
```shell
export SUBJECTS_DIR=your_subject_dir
```
Here are a few files that should be included in $SUBJECTS_DIR

Atlas file. Download lh.HCP-MMP1.annot AND rh.HCP-MMP1.annot, Copy them to the $SUBJECTS_DIR folder. Download link: https://figshare.com/articles/dataset/HCP-MMP1_0_projected_on_fsaverage/3498446 


Subject and fsaverage data. Add subject data and fsaverage data to $SUBJECTS_DIR. Subjects’ structural data should be preprocessed with FreeSurfer. For details please refer:
https://surfer.nmr.mgh.harvard.edu/fswiki/FreeSurfer
https://surfer.nmr.mgh.harvard.edu/fswiki/recon-all
https://surfer.nmr.mgh.harvard.edu/fswiki/FsTutorial/TroubleshootingData

Subject list. Create a text file(sublist.txt, for example) where identifiers of the desired target subjects (named exactly as their corresponding names in $SUBJECTS_DIR) are listed. It should be something that looks like:
  ```shell
  sub01
  sub02
  sub03

  ```

Shell script.Copy create_subj_volume_parcellation.sh and add it to $SUBJECTS_DIR.


Launch shell script
```shell
cd $SUBJECTS_DIR
bash create_subj_volume_parcellation.sh -L your_subject_list -a your_atlas_name -d output_folder

# your_subject_list is the text file created where identifiers of subjects are included
# your_atlas_name: HCP-MMP1

# for example
bash create_subj_volume_parcellation.sh -L sublist.txt -a HCP-MMP1 -d ./output
```
