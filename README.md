# LORIS MRI Downloader for the open PREVENT-AD dataset


## 1. Description

This repository provides a tool to download the open PREVENT-AD MRI files. Users can
choose one of the following tool to download the open PREVENT-AD images:
  - a Python script called `LORIS-MRI-Downloader_PREVENT-AD.py`
  - Jupiter Notebook called `LORIS-MRI_Downloader_PREVENT-AD.ipynb` 

See section 2 below for the installation steps required for the python script 
(section 2.1) and for the Jupiter Notebook (section 2.2).

## 2. Installation and Requirements

Requirements for the script:
- Python (2.7 or 3)
- the following Python libraries: `getpass`, `json`, `requests`, `os`. To install those
libraries using `pip`, run the following commands:

```bash
pip install getpass
pip install json
pip install requests
pip install os
```

## 3. Downloading the MRI from the open PREVENT-AD LORIS API

### 3.1 Using `LORIS-MRI-Downloader_PREVENT-AD.py`

In order to download the images from the open PREVENT-AD LORIS API, run the following
command in the directory where you want the images to be downloaded:

`python LORIS-MRI-Downloader_PREVENT-AD.py`

Note, by default the images will be downloaded in the current working directory. However,
if you wish to download the images in a different directory, you can specify it when 
running the script with the option `-d` as follows:

`python LORIS-MRI-Downloader_PREVENT-AD.py -d %PATH_TO_DIRECTORY%`

with `%PATH_TO_DIRECTORY%` being replaced by the path to the directory where you want
the files to be downloaded.

Additionally, you can specify a list of candidates you wish to download the images
from using the `-l` option.


### 3.2 Using Jupiter Notebook

Open the Jupiter Notebook file `LORIS-MRI_Downloader_PREVENT-AD.ipynb` in Jupiter
Notebook and execute the code in the notebook.



## 4. Organisation of the downloaded structure

