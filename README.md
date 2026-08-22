# Human DNA Promoter Sequence Classifier

## Project Overview
This project implements a machine learning pipeline to identify **human promoter regions** from raw DNA sequences. Promoters are critical genomic markers that initiate gene transcription. This project effectively flags promoter candidates quickly to help with manual validation, which can be time-consuming and expensive. 

The pipeline achieves a **95.45%** verification accuracy using NLP-style tokenization and probablistic modeling.

## Data
[promoters.data](data/promoters.data)

## Pipeline
1. **Data Ingestion**: The data is separated by commas and includes class symbols, names, and sequences. To ingest the data, the pipeline iterates through data file to remove white spaces and separate by commas with a max split of 2. This is to ensure that any additional commas within the sequence will be handled correctly. 

2. **Exploratory Data Analysis (EDA)**: In this step, we validate dataset class balance, assert uniform sequence dimensions, and analyze the structural **_GC Content distribution_** to evaluate biological data integrity. **_GC Content_** is evaluated to help identify promoter regions, which are GC-rich. 

3. **Genomic Tokenization (6-Mers)**: This step transforms sequences into NLP compatible "sentences", consiting of overlapping 6bp tokens. This preserves critical transcription factor binding motifs (6-12bp) and expands vocabulary high-dimensionality to eliminate statistical noise.

4. **Vectorization & Modeling**: Implement robust `CountVectorizer` mapping phase coupled with **Multinomial Naive Bayes Classifier**. Feature transformations, vectorization, are fit exclusively on training data splits to eliminate data leakage.

5. **Production Model Inference**: Perform a production smoke-test module to test pipeline. This is performed on raw, unvetted text inputs, while executing downstream vector transformations and outputs binary predictions alongside explicit statistical confidence metrics.


## Core Performance Metrics
* **Validation Accuracy**: 95.45%

## 🛠️ Installation & Reproduction
```bash
# Clone the repository
git clone https://github.com
cd dna-classifier

# Initialize and activate the isolated virtual environment
python3 -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate

# Install required dependencies
pip install -r requirements.txt

# Run the Jupyter Notebook pipeline
jupyter notebook dna_classifier.ipynb
```