# NCIL BIDS EEG template

This repository serves as a template for EEG studies conducted in the [NeuroCognitive Imaging Lab](http://ncil.science), Department of Psychology & Neuroscience, [Dalhousie University](https://dal.ca), directed by Aaron J Newman](https://aaronjnewman.com).

This contains a BIDS-compliant directory structure, along with scripts (in friendly Jupyter notebook format) to initialize the folder for a study and and also import data. New EEG studies (or studies switching to move to BIDS format) should make a copy of this template and initialize with with study-specific data as described below


# Using this template
- Go to the [template's repository on GitHub](https://github.com/NeuroCognitiveImagingLab/BIDS) and click **Use this template**.
- This will by default want to create a copy of the template as a repository in your personal GitHub account. In general you should not do this, but instead set the owner to `NeuroCognitiveImagingLab` so Aaron and other lab members can manage it after you leave the lab.
- Name the template `BIDS_name_of_study`, where `name_of_study` is replaced with the actual study name. Having the study name in the repo name ensures it's easy to know what's what within the morass of NCIL GitHub repositories.
- Open a terminal window on the NCIL server, navigate to the project's folder. In a browser window, open the GitHub repo page for your copy of the template, click the green **Code** button, and copy the https link. In the  terminal window, type `git clone ` and then past the https link you just copied. Then hit Enter. This will copy the template to the server.
- Edit (at least) the following files:
  - `README.md` (this file) should contain study-specific details (see below), and you can delete these instructions once you're done with them.
  - `config.yml` should be edited to reflect the details of your study. The fields in there will be used to populate the BIDS metadata throughout this directory structure, and be inherited by other scripts (e.g., data import). **It is essential that you edit this script** before doing anything of the steps below.
    - This file is in YAML format. If you're not familiar with it, follow the format you see in the template file, and check out this [beginner's guide](https://circleci.com/blog/what-is-yaml-a-beginner-s-guide/)
- Open Jupyter lab and run the `init_BIDS_study.ipynb` script. You shouldn't typically need to make any changes to the script. This script will initialize the directory structure in a BIDS-compliant manner, creating metadata files based on your edits to `config.yml`
- To import data, copy your raw, unprocessed data files (e.g., raw EEG data files, stimulus presentation log files) to subject-specific directories in `sourcedata`. See the README.md file in that directory for further instructions.

*Edit below to describe your study*


## Study Description


## Stimulus Presentation Details



*Keep the license text below*

---
Code in this project largely relies on the Python pacakges MNE, mne-bids, mne-bids-pipeline. Aditional code written by Aaron J Newman and ---, released under the [BSD 3-clause license](https://opensource.org/licenses/BSD-3-Clause).
