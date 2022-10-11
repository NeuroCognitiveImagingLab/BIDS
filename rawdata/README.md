# `rawdata`
In BIDS, `rawdata` data is the original, unprocessed (or minimally processed due to file format conversion) data in a BIDS-compatible format.

This is distinguished from `sourcedata`, which should contain the original data files as collected by the acquisition systems, such as raw EEG data and stimulus presentation log files.

## Copying data into this BIDS structure
- Make a copy of the template subject directory in `sourcedata` (`sub-00x`) for each subject ID whose data you will import.

*or*

- In the `sourcedata` directory, make a new subdirectory for each participant. Use the naming convention `sub-00x` where 00x is replaced with the subject ID number. Ensure there are always 3 numerals, using 0s to pad (e.g., `sub-003`, *not* `sub-3`)
- Within the subject's directory, create subdirectories for each session (if there is/will be more than one session)
- If there is only one session, create subfolders for each data type (typically `eeg` and `logs`). If there is more than one session, create those subdirectories in each session directory.
- Copy data and log files from the original acquisition system(s) to each subject's `sourcedata` subdirectory.

## Convert data to BIDS format
- Edit the script `code/source2bids.ipynb` to list the subject ID codes of each subject you want to import.
- Run this script
- Outputs are saved to `rawdata`
