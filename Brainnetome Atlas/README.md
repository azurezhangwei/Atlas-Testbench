# Brainnetome: A New Brain Atlas Based on Connectional Architecture.

> Official website: https://atlas.brainnetome.org/index.html

According to the [FreeSurfer document](https://surfer.nmr.mgh.harvard.edu/fswiki/HistoAtlasSegmentation), [Brainnetome Guides](https://atlas.brainnetome.org/download.html) and a [github repo](https://github.com/tannerjared/HCP-MMP1) that converts the Connectome Workbench files to volume masks in native structural space and generates look up tables,
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

  Atlas file. 
  Download BN_Atlas_freesurfer.zip. Unzip BN_atlas_freesurfer.zip and copy the four files: lh.BN_Atlas.gcs , rh.BN_Atlas.gcs ,BN_Atlas_subcortex.gca , and BN_Atlas_246_LUT.txt , to the $SUBJECTS_DIR folder. Download link: https://atlas.brainnetome.org/download.html 


  Subject and fsaverage data. 
  Add subject data and fsaverage data to $SUBJECTS_DIR. Subjects’ structural data should be preprocessed with FreeSurfer. For details please refer:
  https://surfer.nmr.mgh.harvard.edu/fswiki/FreeSurfer
  https://surfer.nmr.mgh.harvard.edu/fswiki/recon-all
  https://surfer.nmr.mgh.harvard.edu/fswiki/FsTutorial/TroubleshootingData

  Subject list. 
  Create a text file(sublist.txt, for example) where identifiers of the desired target subjects (named exactly as their corresponding names in $SUBJECTS_DIR) are listed. It should be something that looks like:
  ```shell
  sub01
  sub02
  sub03

  ```

  Shell script.
  Copy create_subj_volume_parcellation.sh and add it to $SUBJECTS_DIR.

Convert the atlas file to .annot format
```shell
mris_ca_label -l $SUBJECTS_DIR/fsaverage/label/lh.cortex.label fsaverage lh $SUBJECTS_DIR/fsaverage/surf/lh.sphere.reg $SUBJECTS_DIR/lh.BN_Atlas.gcs $SUBJECTS_DIR/fsaverage/label/lh.BN_Atlas.annot

mris_ca_label -l $SUBJECTS_DIR/fsaverage/label/rh.cortex.label fsaverage rh $SUBJECTS_DIR/fsaverage/surf/rh.sphere.reg $SUBJECTS_DIR/rh.BN_Atlas.gcs $SUBJECTS_DIR/fsaverage/label/rh.BN_Atlas.annot

```

Launch shell script
```shell
cd $SUBJECTS_DIR
bash create_subj_volume_parcellation.sh -L your_subject_list -a your_atlas_name -d output_folder

# for example
bash create_subj_volume_parcellation.sh -L sublist.txt -a BN_Atlas -d ./output
```




