# AI4Doc: Document Layout Detection & OCR Pipeline for SEC Filings

[![Python](https://img.shields.io/badge/Python-3.12+-blue.svg)](https://python.org)
[![License](https://img.shields.io/badge/License-All%20Rights%20Reserved-lightgrey.svg)](LICENSE)

A pipeline for collecting, filtering, and annotating SEC regulatory comment letters to build a labeled dataset for document layout detection and OCR.

## What this does

- **Data collection** (`sec_comments.ipynb`): Scrapes SEC.gov for public comment letters across 221 rulemaking dockets, then downloads the PDF attachments (22,278 PDFs collected in this run).
- **Filtering** (`memo.ipynb`): Filters the collected PDFs down to documents that are memorandums, based on the first word of the document text.
- **Dataset construction** (`create_train_val_test_data.ipynb`): Samples 400 pages across the filtered PDFs and splits them into train/val/test (240/80/80, a 60/20/20 ratio). Uses PyMuPDF for native text/layout extraction and falls back to Tesseract OCR for scanned pages.
- **Layout analysis experiments** (`other_scripts/`): Exploratory notebooks testing PubLayNet-based Detectron2 layout detection (via LayoutParser), OpenCV/PyMuPDF-based line segmentation, and annotation workflows using Label Studio, CVAT (through FiftyOne), and LabelBox.

## Tech Stack

Python, PyMuPDF, Tesseract OCR (pytesseract), OpenCV, LayoutParser + Detectron2, FiftyOne, BeautifulSoup, Requests, Playwright, Pandas

## Project Structure

```
ai4doc/
├── sec_comments.ipynb                   # SEC data scraping and collection
├── memo.ipynb                           # Document classification and filtering
├── create_train_val_test_data.ipynb     # Train/val/test dataset generation
└── other_scripts/                       # Layout detection & annotation experiments
    ├── layout_parser.ipynb              # Detectron2 / LayoutParser testing
    ├── pytesseract.ipynb                # OCR testing
    ├── line_segmentation.ipynb          # Line segmentation via OpenCV
    └── fiftyone.ipynb                   # CVAT annotation workflow via FiftyOne
```

## Setup

```bash
conda create -n py312sec python=3.12
conda activate py312sec
pip install -r requirements.txt
```

Tesseract OCR must be installed separately (see [PyMuPDF's OCR setup docs](https://pymupdf.readthedocs.io/en/latest/installation.html)) and the `TESSDATA_PREFIX` environment variable set to your local tessdata folder.

Raw PDFs and generated datasets are not included in this repository; the notebooks regenerate them from SEC.gov when run.

## Author

Akshay Sharma

## License

All Rights Reserved — see [LICENSE](LICENSE).
