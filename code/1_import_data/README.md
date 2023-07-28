# 1_import_data

This folder contains the scripts used to import data into the BIDS project. 

`0_import_sourcedata` will copy original data from another location on the server to the `sourcedata` folder for this project. This is typically only necessary for older data sets that were not originally stored in the BIDS format.

`1_eeg2bids` will convert the eeg data in `sourcedata` to a BIDS-compliant format, in the `rawdata` folder

`2_beh2bids` will copy behavioural log files associated with each EEG file from `sourcedata` to `rawdata`, and give them BIDS-compliant file names