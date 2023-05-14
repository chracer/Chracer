# *Chracer*

*Chracer* is a proof-of-concept tool. *Chracer* uses object layout information obtained from the PDB to extract forensically meaningful information from Chromium's virtual memory. **Because *Chracer* is not yet optimized, some code is hard-coded.**

# Dataset

## Minidumps

The Google Driver link that shares minidumps corresponding to experiment cases
> https://drive.google.com/drive/folders/11rEJ41PsUZBDKKhDYjrpVotb0qU7vomk?usp=sharing

## Symbols

Thie Mega links that share parsed symbol files of _chrome.dll_ and _content.dll_ of Chromium (version 113.0.5650.0, commit fed2d65)
> https://mega.nz/file/QZ9iXLzB#hkSugGvES17dO0W3AgGW0JSt5nLbP0TNXCMtsnrHFco
> https://mega.nz/file/YJ000Q6A#r6ERyaucP60P_fkjTdrlqKeVZ_1hutQEzEXUMyQE7yA

# Usage

We developed the tools based on Python 3.7.9.

## Setup

In Linux:
```
$ git clone https://github.com/chracer/Chracer.git
$ cd Chracer
$ python3 -m venv venv
$ source venv/bin/activate
(venv) $ pip install -r requirements.txt
```

In Windows:
```
> git clone https://github.com/chracer/Chracer.git
> cd Chracer
> python -m venv venv
> venv\Scripts\activate
(venv) > pip install -r requirements.txt
```

## Download datasets

1. Storing minidumps files to _dumps_ directory after downloading them
2. Sotring parsed symbol files to _symbols_ directory after downloading them
3. After completing the download, it should have a folder tree like the one below
    ```
    Chracer/
    +  chracer/
    |  +  ...
    +  dumps/
    |  +  case_google_chrome.dmp
    |  +  case_microsoft_edge.dmp
    |  +  case1.dmp
    |  +  case2.dmp
    |  +  case3.dmp
    |  +  case4.dmp
    |  +  case5.dmp
    +  symbols/
    |  +  chrome.dll.pdb.xml
    |  +  content.dll.pdb.xml
    +  case1.py
    +  case2.py
    +  case3.py
    +  case4.py
    +  case5.py
    +  finder.py
    +  case_google_chrome.py
    +  case_microsoft_edge.py
    +  README.md
    +  requirements.txt
    ```

## Case 1

In this case, the tool extracts session id of each _Browser_ object, tab, document title, URL from _dumps/case1.dmp_. 

```
(venv) $ python3 case1.py
```

## Case 2

In this case, the tool extracts tab group-related information from _dumps/case2.dmp_.

```
(venv) $ python3 case2.py
```

## Case 3

In this case, the tool extracts visited URL-related information from _dumps/case3.dmp_.

```
(venv) $ python3 case3.py
```

## Case 4

In this case, the tool extracts SSL certificate-related information from _dumps/case4.dmp_ (this file is same to _dumps/case3.dmp_).

```
(venv) $ python3 case4.py
```

## Case 5

In this case, the tool extracts visited URL and distinguishes whether discovered _Browser_ object is a private mode or not.

```
(venv) $ python3 case5.py
```

## Case Google Chrome

In this case, the tool extracts visited URL-related information from _dumps/case\_google\_chrome.dmp_ by adjusting offset of fields of some classes.

```
(venv) $ python3 case_google_chrome.py
```

## Case Microsoft Edge

In this case, the tool extracts visited URL-related information from _dumps/case\_microsoft\_edge.dmp_ by adjusting offset of fields of some classes.

```
(venv) $ python3 case_microsoft_edge.py
```

## Finder

This code takes a minidump file as input. After it discovers a _Browser_ object from virtual memory dumped in minidump, it extracts visited URL-related information.

```
(venv) $ python3 finder.py dumps/case1.dmp
```

# Notes

System requirements
- 32GB of RAM
- At least 50GB of free disk space