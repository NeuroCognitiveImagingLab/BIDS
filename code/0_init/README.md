# Initialize sutdy metadata for an EEG BIDS project 

Before you run this file, be sure to edit `config.json` to reflect the details of your study.

The script `0_init_BIDS_study.ipynb` will initialize the BIDS project by reading the `config.json` file using the information to generate a BIDS-compliant `dataset_description.json` file.

This file should typically only be run once for a project, unless you make an error.
