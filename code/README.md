# `code` directory
The `code` directory should store all code that is used to operate on (import, convert, process, analyze, etc.) the data in the BIDS directory structure. This directory can further be organized into subfolders according to different processing pipelines, analyses, etc.

And data or other output that is produced by files in the `code` folder should generally go in the `derivatives` folder, with the exceptions of file format conversion (which should generally output to `sourcedata`) and data import scripts (which should generally output to `rawdata`).
