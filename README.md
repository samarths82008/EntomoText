🦋 Entomology Label OCR Pipeline
Automated pipeline for extracting structured data from entomological specimen label photographs using computer vision and OCR.
What This Does
Natural history museums hold millions of pinned insect specimens. Each one has small paper labels recording where, when, and by whom it was collected — data that is invaluable for biodiversity research but almost entirely undigitized. This project automates that transcription.
Detection → OCR → Structured Data

A custom Roboflow model detects and localizes individual label regions within specimen photographs
Each crop is preprocessed and passed to Tesseract OCR
Raw text is parsed into Darwin Core fields and exported as CSV

Pipeline
Specimen Image
      │
      ▼
Roboflow Model (entamology/6)
  → bounding boxes around each label
      │
      ▼
Preprocessing (upscale, deskew, binarize)
  → clean crops for OCR
      │
      ▼
Tesseract OCR
  → raw text per label region
      │
      ▼
Darwin Core Parser
  → scientificName, locality, stateProvince,
     county, eventDate, recordedBy,
     verbatimElevation, samplingProtocol
      │
      ▼
CSV Export
Fields Extracted
FieldExamplecatalogNumberEMEC123456scientificNamePterostichus lamalocalityBlodgett Experimental ForeststateProvinceCaliforniacountyEl Dorado CountyeventDate16-18 September 2011recordedByD.H. KavanaughverbatimElevation1300 msamplingProtocolhand collecting
Data Source
Specimen images are fetched via the iDigBio API — no login required. Currently targeting CAS (California Academy of Sciences) arthropod records as a development dataset, with the Essig Museum of Entomology (EMEC) as the primary target collection.
Setup
Open in Google Colab and run cells in order. All dependencies are installed in cell 1.
Requirements installed automatically:

inference-sdk — Roboflow inference
pytesseract + tesseract-ocr — OCR
opencv-python-headless — image preprocessing
pandas, requests, tqdm

You need:

A Roboflow API key (set in cell 2)
Internet access (for iDigBio image downloads and Roboflow inference)

Status
ComponentStatusLabel region detection✅ Working (~0.81 avg confidence)Image download via iDigBio✅ WorkingOCR preprocessing🔧 In progress — quality varies by imageDarwin Core parsing🔧 In progress — parser being tightenedEMEC direct access❌ Server blocks Colab IPs
End Goal
A generalizable tool any natural history museum can run on their digitization workflow — input a folder of specimen images, output a Darwin Core CSV ready for import into a collection management system or aggregator like iDigBio or GBIF.
Background
Entomological collections are an irreplaceable archive of biodiversity. Many specimens represent species or populations that no longer exist at their original collection sites. Getting this data out of handwritten labels and into queryable databases is a conservation problem as much as a digitization one.

Built with Roboflow · iDigBio · Tesseract
