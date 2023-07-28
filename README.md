# NCIL BIDS EEG template

This repository serves as a template for EEG studies conducted in the [NeuroCognitive Imaging Lab](http://ncil.science), Department of Psychology & Neuroscience, [Dalhousie University](https://dal.ca), directed by Aaron J Newman](https://aaronjnewman.com).

This contains a BIDS-compliant directory structure, along with scripts (in friendly Jupyter notebook format) to initialize the folder for a study and and also import data. New EEG studies (or studies switching to move to BIDS format) should make a copy of this template and initialize with with study-specific data as described below

# About BIDS
[BIDS](https://bids.neuroimaging.io) is a standard for organizing neuroimaging data, including EEG. It is a set of conventions for how to organize data files and metadata, and is designed to be flexible enough to accommodate a wide range of experimental paradigms and data types. It is designed to be easy to use, and to facilitate data sharing and reproducible research.

The BIDS structure for an EEG study looks something like this:

```
— code
    - 0_init
    - 1_import_data
    - 2_preprocessing_erp
    - 3_visualization_erp
    - 4_measurement_erp
    - 5_stats_erp
    - 6_classification
    - 7_stats_classification

- derivatives
    - preprocessing_pipeline_1
        - s001
        - s002
    - preprocessing_pipeline_2
    - statistical_analysis_1
      - ERP_component_1
        - data
        - figures
        - tables
    - classification_analysis_1
      - classifier_1
        - data
        - figures
        - tables
        
- rawdata
    - s001
      - ses-1
        - beh
        - eeg
      - ses-2
    - s002
        
- sourcedata
    - sub-001
      - ses-1
        - beh
        - eeg
      - ses-2
    - sub-002

- config.yml
- dataset_description.json
- README.md


```

- `config.yml` is a configuration file that contains metadata about the study. This includes things like the name of the study, the name of the PI, the name of the lab, etc. This file is used to populate the metadata files in the BIDS directory structure, and is also used by scripts to populate metadata in the data files themselves. **This file should be edited to reflect the details of your study.**
- `code` contains all code used to operate on the data sets, including file conversion/import, preprocessing, and analysis
- `sourcedata` contains the original, unprocessed data files, organized into subfolders by modality (e.g., EEG, behavioural log files). These files should be write-protected as the original data should never be modified or deleted. In general, if a BIDS dataset is shared publicly, this folder should not be included, as it may contain sensitive information. However, it is useful to keep a copy of the original data in case it needs to be reprocessed.
- `rawdata` contains BIDS-compliant raw datasets. These are typically the output of an import script that operates on data in `sourcedata` and converts it to BIDS-compliant formats.
- `derivatives` contain versions of the data that are processed by scripts in the `code` folder. Separate folders in `derivatives` should be made for different types of outputs, e.g., the output of a preprocessing pipeline would go in one folder, but a statistical analysis on that preprocessed data in another. This organization makes it easy to perform different batches of operations on data and compare the results, as well as keeping things organized. Within a `derivatives` subfolder, data from individuals should be organized by subject, potentially under subfolders for the outputs of different preprocessing steps, if these are saved. Aggregated data (e.g., exploratory data analysis, statistical analysis) should be saved in subfolders under the relevant analysis step.
- `README.md` is a Markdown file which you should edit to include a descirption of the study and experimental paradigm. This provides the context in which the data can be understood. You are currently reading the README file for this template, which you should edit to reflect the details of your study.


# Using this template

**Note:** this template relies on your having set up GitHub on your server account. This is not entirely trivial because you need to set up SSH keys. If you haven't done this, follow the instructions [here](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh). If you have any problems, ask Aaron for help.

- Go to the [template's repository on GitHub](https://github.com/NeuroCognitiveImagingLab/BIDS) and click **Use this template**.
- This will by default want to create a copy of the template as a repository in your personal GitHub account. In general you should not do this, but instead set the owner to `NeuroCognitiveImagingLab` so Aaron and other lab members can manage it after you leave the lab.
- Name the template `BIDS_name_of_study`, where `name_of_study` is replaced with the actual study name. Having the study name in the repo name ensures it's easy to know what's what within the morass of NCIL GitHub repositories.
- Open a terminal window on the NCIL server, navigate to the project's folder. In a browser window, open the GitHub repo page for your copy of the template, click the green **Code** button, and copy the https link. In the  terminal window, type `git clone ` and then past the https link you just copied. Then hit Enter. This will copy the template to the server.
- Edit (at least) the following files:
  - `README.md` (this file) should contain study-specific details (see suggested headings below). Since you are currently reading the template's README.md file, you will need to delete these instructions once you're done with them.
  - `config.yml` should be edited to reflect the details of your study. The fields in there will be used to populate the BIDS metadata throughout this directory structure, and be inherited by other scripts (e.g., data import). **It is essential that you edit this script** before doing anything of the steps below.
    - This file is in YAML format. If you're not familiar with it, follow the format you see in the template file, and check out this [beginner's guide](https://circleci.com/blog/what-is-yaml-a-beginner-s-guide/)
- Open Jupyter lab and run the `init_BIDS_study.ipynb` script. You shouldn't typically need to make any changes to the script. This script will initialize the directory structure in a BIDS-compliant manner, creating metadata files based on your edits to `config.yml`
- To import data, copy your raw, unprocessed data files (e.g., raw EEG data files, stimulus presentation log files) to subject-specific directories in `sourcedata`. See the README.md file in that directory for further instructions.

## Study Description
*Edit  to describe your study*

## Stimulus Presentation Details
*Edit  to describe your study*


---
Code in this project largely relies on the Python pacakges MNE, mne-bids, mne-bids-pipeline. Aditional code written by Aaron J Newman, released under the [BSD 3-clause license](https://opensource.org/licenses/BSD-3-Clause).
