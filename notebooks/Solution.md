# 🥉Kaggle Make-Data-Count - Finding-Data-References Bronze (My Solution)

## Overview
This repository showcases my solution for the Kaggle competition “Make Data Count - Finding Data References.” The challenge is to detect mentions of datasets in scientific papers and categorize them as Primary (created by the authors for the study) or Secondary (reused from existing sources).

Competition link: [Make Data Count - Finding Data References](https://www.kaggle.com/competitions/make-data-count-finding-data-references/overview)

## Goal
The objective of this project is to develop a robust pipeline that:
* Reads and analyzes scientific papers in PDF and XML format.
* Detects references to datasets, including DOIs, repository names, and accession numbers.
* Categorizes each dataset mention as Primary or Secondary.
* Generates output in the required submission format (article_id, dataset_id, type).

## Approach
This project leverages text parsing, regular expressions, and language model-based classification to identify and categorize references to datasets in scientific papers.

### 1. Environment Setup
* Resolves conflicts between packages (e.g., TensorFlow) and enforces specific versions for parsing, LLM inference, and regex operations.
* Includes safeguards for handling CUDA, logging, and I/O peculiarities on Kaggle.

### 2. Helper & Logging ('helpers.py')
helpers.py is a utility module designed to streamline data processing and evaluation in Kaggle competitions. It provides functions for automatic Kaggle environment detection and directory setup, text data loading and normalization, dataset type classification (Primary/Secondary), and F1 score calculation for submitted data.

### 3. PDF and XML Parsing ('parse.py')
parse.py is a document parser for Kaggle competitions. It automatically detects and converts PDF and XML files into plain text, saving standardized text to /tmp/train_parse/<article_id>.txt. The script detects XML formats, extracts main text and references, normalizes DOI notation, and appends XML content to the PDF text when both are present.

### 4. Parsing validation tool ('check_parse.py')
check_parse.py is a validation script that checks the parsing results. It verifies whether the dataset_id values from the training labels (train_labels.csv) are correctly present in the parsed text data (train_parse). Missing IDs are reported in the logs, helping ensure that the parser works as expected.

### 5. Dataset ID extraction tool from research text ('getid.py')
getid.py is a script for extracting dataset identifiers (DOIs, accession numbers, etc.) from research articles. It splits body text and references, applies regex-based matching to detect and normalize dataset IDs, removes noise, and saves the extracted results to Parquet and CSV files. It also captures context windows around each match to help verify the usage of identified datasets.

### 6. LLM-based dataset ID classification tool ('llm_validate.py')
llm_validate.py uses a large language model (`Qwen2.5-32B` AWQ quantized) to classify extracted DOIs and accession numbers. It categorizes them as A (Data) if they correspond to dataset repositories, or B (Literature) if they belong to publications. The validated results are merged and exported to the final submission file (submission.csv).

