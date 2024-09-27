# HCPMMP1.0	
> Official website: https://surfer.nmr.mgh.harvard.edu/fswiki/CorticalParcellation_Yeo2011

According to the [FreeSurfer document](https://surfer.nmr.mgh.harvard.edu/fswiki/HistoAtlasSegmentation), [Brainnetome Guides](https://atlas.brainnetome.org/download.html) and a github [repo](https://github.com/tannerjared/HCP-MMP1) that converts the Connectome Workbench files to volume masks in native structural space and generates look up tables,
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

Atlas file. There are two versions of this atlas, a 7-network parcellation and a 17-network parcellation. Download Yeo_JNeurophysiol11_FreeSurfer.zip. Unzip it and copy the four files in fsaverage/label/ folder: lh.Yeo2011_7Networks_N1000.annot , rh.Yeo2011_7Networks_N1000.annot , lh.Yeo2011_17Networks_N1000.annot and rh.Yeo2011_17Networks_N1000.annot , to the $SUBJECTS_DIR folder. Download link: http://surfer.nmr.mgh.harvard.edu/pub/data/Yeo_JNeurophysiol11_FreeSurfer.zip 


Subject and fsaverage data. Add subject data and fsaverage data to $SUBJECTS_DIR. Subjects’ structural data should be preprocessed with FreeSurfer. For details please refer:
https://surfer.nmr.mgh.harvard.edu/fswiki/FreeSurfer
https://surfer.nmr.mgh.harvard.edu/fswiki/recon-all
https://surfer.nmr.mgh.harvard.edu/fswiki/FsTutorial/TroubleshootingData

Subject list. Create a text file(sublist.txt, for example) where identifiers of the desired target subjects (named exactly as their corresponding names in $SUBJECTS_DIR) are listed.

Shell script.Copy create_subj_volume_parcellation.sh and add it to $SUBJECTS_DIR.


Launch shell script
```shell
cd $SUBJECTS_DIR
bash create_subj_volume_parcellation.sh -L your_subject_list -a your_atlas_name -d output_folder

# your_subject_list is the text file created where identifiers of subjects are included
# your_atlas_name: Yeo2011_7Networks_N1000 or Yeo2011_17Networks_N1000

# for example
bash create_subj_volume_parcellation.sh -L sublist.txt -a Yeo2011_7Networks_N1000 -d ./output
```



