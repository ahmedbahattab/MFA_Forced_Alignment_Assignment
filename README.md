# **README.md — Forced Alignment using Montreal Forced Aligner (MFA)**

### *Assignment 1 – Speech Processing*

<div align="center" style="text-align: center">
<h2>Speech Processing – Forced Alignment Assignment</h2>
<p><strong>Using Montreal Forced Aligner (MFA)</strong></p>

<img src="https://img.shields.io/badge/Tool-MFA%203.3.8-blue">
<img src="https://img.shields.io/badge/Environment-Conda-yellow">
<img src="https://img.shields.io/badge/Language-English_US_ARPA-green">
<img src="https://img.shields.io/badge/Visualization-Praat-purple">
</div>

---

## **Contents**

* [Objective](#objective)
* [1. Environment Setup](#1-environment-setup)
* [2. Downloading MFA Models](#2-downloading-required-models)
* [3. Dataset Preparation](#3-dataset-preparation)
* [4. Running Forced Alignment](#4-run-forced-alignment)
* [5. Corpus Validation](#5-validation)
* [6. Praat TextGrid Analysis](#6-inspect--analyze-output-in-praat)
* [7. Output Files](#7-output-files-included)
* [8. Screenshots](#8-screenshots-included)
* [Tools Used](#tools-used)
* [Observations](#observations)
* [Conclusion](#conclusion)

---

## **Objective**

The purpose of this assignment is to:

* Set up Montreal Forced Aligner (MFA)
* Align audio (.wav) with transcripts (.txt)
* Generate Praat TextGrid files containing word & phoneme timestamps
* Learn how automatic phonetic alignment works

MFA takes:
🎤 **Audio** → 🔤 **Transcript** → **TextGrid (word + phoneme alignment)**

---

# **1. Environment Setup**

### Create & activate environment

```bash
conda create -n mfa_env python=3.9
conda activate mfa_env
```

### Install MFA

```bash
pip install montreal-forced-aligner
```

### Verify installation

```bash
mfa version
```

MFA 3.3.8 successfully installed.

---

# **2. Downloading Required Models**

### Dictionary

```bash
mfa model download dictionary english_us_arpa
```

### Acoustic Model

```bash
mfa model download acoustic english_us_arpa
```

### Verify

```bash
mfa model list dictionary
mfa model list acoustic
```

Models downloaded correctly.

---

# **3. Dataset Preparation**

The dataset contained:

* `/wav` → speech audio
* `/transcripts` → text files

These were reorganized to MFA format:

```
corpus_ready/
│── sample1.wav
│── sample1.txt
│── sample2.wav
│── sample2.txt
│── ...
```

All files were paired and prepared correctly.

---

# **4. Run Forced Alignment**

Main command used:

```bash
mfa align "[OPTIONS] CORPUS_DIRECTORY DICTIONARY_PATH ACOUSTIC_MODEL_PATH
          OUTPUT_DIRECTORY"
```

MFA executed:

* Feature extraction
* G2P & graph compilation
* First-pass alignment
* Viterbi alignment
* TextGrid export

Alignment completed successfully.

---

# **5. Validation**

Command:

The general syntax is:
```bash
mfa validate <corpus_directory> <dictionary> <acoustic_model>
```
Example:
```bash
mfa validate C:\Users\Ahmed\Desktop\Corpus english_us_arpa english_us_arpa
```

Validation output:

* 6 audio files
* 6 transcripts
* No missing files
* No audio read errors
* Minor OOV warnings (expected)

Corpus passed validation.

---

# **6. Inspect & Analyze Output in Praat**

Every generated `.TextGrid` was:

* Checked for word tier alignment
* Checked for phoneme tier alignment
* Compared with spectrogram
* Verified with waveform timing

All TextGrids aligned accurately, with no major mismatches.

---

# **7. Output Files Included**

```
alignment_output/
│── file1.TextGrid
│── file2.TextGrid
│── file3.TextGrid
│── ...
│── alignment_analysis.csv
```

Includes:

* TextGrid files
* CSV analysis data (durations, likelihoods, SNR)

---

# **8. Screenshots Included**

Located in `/screenshots/`:

* MFA installation
* Model downloads
* Validation results
* Alignment logs
* Praat TextGrid views

---

# **Tools Used**

| Tool / Technology                          | Purpose                                     |
| ------------------------------------------ | ------------------------------------------- |
| **Python**                                 | Runs MFA inside Conda environment           |
| **Miniconda**                              | Creates `mfa_env` virtual environment       |
| **MFA (Montreal Forced Aligner)**          | Performs forced alignment                   |
| **MFA Acoustic Model (english_us_arpa)**   | Acoustic features for aligning phonemes     |
| **MFA Dictionary Model (english_us_arpa)** | Converts words → phonemes                   |
| **Praat**                                  | Visual inspection of alignment in TextGrids |

---

# **Observations**

* Alignment was accurate and consistent
* Word boundaries matched the waveform
* Phoneme segmentation was clean
* Minor OOV warnings did not affect alignment
* No timing offsets or missing segments

---

# **Conclusion**

The complete forced alignment pipeline using MFA was successfully executed, including:

* Environment setup
* Dataset preparation
* Dictionary & acoustic model download
* Forced alignment
* TextGrid verification in Praat
