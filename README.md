# 🦋 Entomology Label OCR Pipeline

An automated computer vision + OCR pipeline for extracting structured biodiversity data from entomological specimen label photographs.

Natural history museums house millions of pinned insect specimens, each with tiny paper labels containing critical collection metadata. This project automates the transcription of those labels into machine-readable Darwin Core records.

---

## Overview

This pipeline converts a specimen photograph into structured biodiversity metadata.

```text
Specimen Image
    ↓
Roboflow Detection Model
    ↓
Label Bounding Boxes
    ↓
Image Preprocessing
(upscale, deskew, binarize)
    ↓
Tesseract OCR
    ↓
Raw Label Text
    ↓
Darwin Core Parser
    ↓
Structured CSV Output
```

---

## Features

- Automated label detection using Roboflow
- OCR powered by Tesseract
- Image preprocessing for improved transcription accuracy
- Darwin Core metadata extraction
- CSV export for downstream biodiversity workflows
- Designed for museum-scale digitization

---

## Extracted Fields

The parser currently extracts the following Darwin Core fields:

- `catalogNumber`
- `scientificName`
- `locality`
- `stateProvince`
- `county`
- `eventDate`
- `recordedBy`
- `verbatimElevation`
- `samplingProtocol`

### Example Output

```csv
catalogNumber,scientificName,locality,stateProvince,county,eventDate,recordedBy,verbatimElevation,samplingProtocol
EMEC123456,Pterostichus lama,Blodgett Experimental Forest,California,El Dorado County,2011-09-16,D.H. Kavanaugh,1300 m,hand collecting
```

---

## Data Sources

Specimen images are retrieved through the iDigBio API (no authentication required).

Current development datasets include:

- California Academy of Sciences (CAS)
- Essig Museum of Entomology (EMEC)

---

## Installation

This project is designed to run in Google Colab.

### Dependencies

```bash
pip install inference-sdk pytesseract opencv-python-headless pandas requests tqdm
```

You must also install:

- Tesseract OCR

---

## Requirements

- Roboflow API key
- Internet connection
- Google Colab (recommended)

Set your Roboflow API key in the configuration cell before running the notebook.

---

## Current Status

| Component | Status |
|----------|--------|
| Label Detection | ✅ Working (~0.81 average confidence) |
| iDigBio Image Download | ✅ Working |
| OCR Preprocessing | 🔧 In Progress |
| Darwin Core Parsing | 🔧 In Progress |
| EMEC Direct Access | ❌ Blocked by Colab IP restrictions |

---

## End Goal

A general-purpose digitization tool that any natural history museum can deploy.

### Input

- Folder of specimen images

### Output

- Darwin Core-compliant CSV

Ready for import into:

- Collection management systems
- iDigBio
- GBIF
- Institutional databases

---

## Why This Matters

Entomological collections are irreplaceable biodiversity archives. Many specimens document populations and habitats that have changed dramatically—or vanished entirely.

Digitizing specimen labels transforms inaccessible handwritten records into searchable scientific data, enabling:

- Biodiversity research
- Conservation planning
- Climate change analysis
- Species distribution modeling
- Historical biogeography

---

## Tech Stack

- Python
- Roboflow
- Tesseract OCR
- OpenCV
- iDigBio API
- Pandas

---

## Repository Structure

```text
.
├── notebook.ipynb
├── output/
├── sample_images/
└── README.md
```

---

## Future Improvements

- Fine-tune OCR for historical handwriting
- Support multiple label layouts
- Batch processing at museum scale
- Direct GBIF/iDigBio export
- Web application interface

---

## Acknowledgments

- Roboflow
- iDigBio
- Essig Museum of Entomology
- California Academy of Sciences

---

## License

MIT License
