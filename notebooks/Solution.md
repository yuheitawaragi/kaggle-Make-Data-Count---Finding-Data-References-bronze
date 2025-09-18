# Kaggle Make-Data-Count - Finding-Data-References Bronze (My Solution)

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



