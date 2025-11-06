# **Forced Alignment using Montreal Forced Aligner (MFA)**  
### *Assignment 1 – Speech Processing*

<div align="center" style="text-align: center">
<h2>Speech Processing – Forced Alignment Assignment</h2>
<p><strong>Using Montreal Forced Aligner (MFA)</strong></p>

<img src="https://img.shields.io/badge/Tool-MFA%203.3.8-blue">
<img src="https://img.shields.io/badge/Environment-Miniconda-yellow">
<img src="https://img.shields.io/badge/Acoustic_Model-English_US_ARPA-6a5acd">
<img src="https://img.shields.io/badge/Dictionary-English_US_ARPA-9b59b6">
<img src="https://img.shields.io/badge/Visualization-Praat-purple">
</div>

---

## **Contents**
- [Objective](#objective)
- [1. Environment Setup](#1-environment-setup)
- [2. Downloading MFA Models](#2-downloading-required-models)
- [3. Dataset Preparation](#3-dataset-preparation)
- [4. Corpus Validation](#4-validation)
- [5. Running Forced Alignment](#5-run-forced-alignment)
- [6. Praat TextGrid Analysis](#6-inspect--analyze-output-in-praat)
- [7. Output Files](#7-output-files-included)
- [8. Screenshots](#8-screenshots-included)
- [Tools Used](#tools-used)
- [Observations](#observations)
- [Conclusion](#conclusion)

---

## **Objective**
This assignment required setting up and running the full Montreal Forced Aligner pipeline.  
My goals were to:

- Install and configure MFA inside a clean Conda environment  
- Prepare a small speech corpus containing `.wav` files and matching transcripts  
- Perform forced alignment using the **english_us_arpa** dictionary and acoustic model  
- Generate aligned TextGrid files  
- Visually analyze the alignment using **Praat**

In short:

🎤 **Speech Audio** → 🔤 **Transcript** → ✅ **Word + Phoneme Alignment (TextGrid)**

---

# **1. Environment Setup**

### Create & activate a dedicated environment
```bash
conda create -n mfa_env python=3.9
conda activate mfa_env
````

### Install MFA

```bash
pip install montreal-forced-aligner
```

### Verify installation

```bash
mfa version
```

I confirmed that MFA 3.3.8 installed successfully.

---

# **2. Downloading Required Models**

### Download dictionary

```bash
mfa model download dictionary english_us_arpa
```

### Download acoustic model

```bash
mfa model download acoustic english_us_arpa
```

### Verify models

```bash
mfa model list dictionary
mfa model list acoustic
```

Both models appeared in the list, confirming that the installation was correct.

---

# **3. Dataset Preparation**

My dataset contained:

* `/wav` — raw audio files
* `/transcripts` — matching text transcripts

I reorganized them into the standard MFA structure:

```
corpus_ready/
│── sample1.wav
│── sample1.txt
│── sample2.wav
│── sample2.txt
│── ...
```

All files were paired properly (each `.wav` had a `.txt` with the same base name).

---

# **4. Validation**

Before aligning, I validated the corpus using:

```bash
mfa validate <corpus_directory> <dictionary_path_or_name> <acoustic_model_path_or_name>
```
```bash
mfa validate C:\Users\Ahmed\Desktop\Corpus english_us_arpa english_us_arpa
```

**Validation results:**

* 6 audio files detected
* 6 matching transcripts found
* No unreadable audio
* Minor OOV warnings (expected)

The corpus passed validation with no critical issues.

---

# **5. Run Forced Alignment**

General syntax:

```bash
mfa align [OPTIONS] CORPUS DICTIONARY ACOUSTIC_MODEL OUTPUT
```

My command:

```bash
mfa align C:\Users\Ahmed\Desktop\Corpus english_us_arpa english_us_arpa C:\Users\Ahmed\Desktop\Aligned_Output
```

During alignment, MFA performed:

* Feature extraction
* G2P for any unknown words
* Graph compilation
* First-pass + Viterbi alignment
* TextGrid generation

The alignment completed successfully without errors.

---

# **6. Inspect & Analyze Output in Praat**

To evaluate the alignments, I opened each `.TextGrid` in **Praat**:

Download [Praat](https://praat.org/) from the official website.

What I checked:

* Word boundaries matched the waveform
* Phoneme tier had clean segmentation
* No overlapping or missing intervals
* Pauses and silences aligned correctly
* Compared alignment with spectrogram for accuracy

Overall, the TextGrids looked consistent and well-aligned.

---

# **7. Output Files Included**

```
alignment_output/
│── sample1.TextGrid
│── sample2.TextGrid
│── sample3.TextGrid
│── ...
│── alignment_analysis.csv
```

Deliverables include:

* All generated TextGrid files
* CSV alignment statistics (duration, confidence, likelihoods)

---

# **8. Screenshots Included**

Screenshots are stored in the `/screenshots` folder:

* MFA installation
* Model downloads
* Corpus validation
* Alignment logs
* Praat TextGrid views

These provide visual proof of each step in the pipeline.

---

# **Tools Used**

| Tool / Technology                  | Purpose                                  |
| ---------------------------------- | ---------------------------------------- |
| **Python 3.9**                     | Environment for running MFA              |
| **Miniconda**                      | Managing isolated MFA environment        |
| **MFA 3.3.8**                      | Forced alignment engine                  |
| **english_us_arpa Dictionary**     | Grapheme-to-phoneme mapping              |
| **english_us_arpa Acoustic Model** | Acoustic prediction for alignment        |
| **Praat**                          | Visual inspection of TextGrid alignments |

---

# **Observations**

* All audio files aligned without failure
* Word and phoneme boundaries were accurate
* OOV warnings were minimal and had no effect
* No timing drift or segmentation issues
* Alignment quality was consistent across all files

---

# **Conclusion**

I successfully completed the full forced alignment workflow:

* Environment setup
* Dataset preparation
* Dictionary & acoustic model setup
* Corpus validation
* Forced alignment using MFA
* TextGrid verification in Praat
---
