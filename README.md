Privacy Preserving Synthetic Data Generation on Full MIMIC III Dataset
Overview

This repository presents a scalable, privacy preserving synthetic data generation pipeline built on the full MIMIC III clinical database.

The project extends beyond a single table and implements synthetic data generation, evaluation, and downstream validation across multiple structured healthcare tables including:

ADMISSIONS

PATIENTS

DIAGNOSES_ICD

D_ICD_DIAGNOSES

CPTEVENTS

LABEVENTS

MICROBIOLOGYEVENTS

TRANSFERS

SERVICES

INPUTEVENTS

And additional structured tables

The work is grounded in our research paper:

Synthetic Data Generation for Healthcare
Department of Computer Science
California State Polytechnic University, Pomona

As described in the paper 

Synthetic Data Generation in He…

, we developed a TVAE based pipeline using the SDV framework to generate statistically faithful and machine learning useful synthetic healthcare data.

What is MIMIC III?

MIMIC III (Medical Information Mart for Intensive Care III) is a large, publicly available critical care database developed by MIT and hosted on PhysioNet.

It contains:

Over 60,000 ICU admissions

Demographics

Admission records

Diagnoses and procedures

Lab measurements

Medications

Clinical notes

Mortality indicators

Although de identified, MIMIC III remains sensitive healthcare data and requires credentialed access due to HIPAA regulations.

It is widely used for:

Clinical machine learning research

Mortality prediction

Risk stratification

Time series modeling

Healthcare analytics benchmarking

Research Motivation

Healthcare data access is heavily restricted due to HIPAA and privacy laws.

As discussed in our paper 

Synthetic Data Generation in He…

:

Real patient data is difficult to share

Model reproducibility becomes challenging

Academic experimentation is limited

Industrial prototyping slows down

Synthetic data provides a solution by:

Preserving statistical properties

Removing personally identifiable information

Retaining predictive utility

Enabling privacy compliant experimentation

Research Contribution

This project delivers:

End to end preprocessing pipelines for multiple MIMIC III tables

TVAE based synthetic generation

CTGAN comparison experiments

Statistical validation

Machine learning utility validation

Correlation structure preservation analysis

Multi table extension beyond admissions

RandomForest trained on real data achieved 86 percent accuracy

RandomForest trained on synthetic data achieved 84 percent accuracy

Correlation structures were largely preserved

Feature distributions closely matched

This demonstrates minimal predictive degradation while maintaining privacy safety.

Methodology
1 Data Preprocessing

Missing value imputation

Removal of high missing columns

Label encoding for categorical variables

StandardScaler normalization for numerical features

Metadata detection using SDV SingleTableMetadata

2 Model Architecture

We primarily used:

TVAE – Tabular Variational Autoencoder

Encoder → latent space → decoder

Reparameterization trick

ELBO loss (reconstruction + KL divergence)

Optimized for mixed type tabular healthcare data

TVAE was selected because:

Stable training

Lower memory requirements

Works well in Jupyter environments

Suitable for large tabular healthcare datasets

CTGAN was evaluated but proved resource intensive for full table training on local systems.

Synthetic Data Generation Workflow

For each table:

Load raw CSV from MIMIC III

Clean and preprocess

Detect metadata schema

Train TVAESynthesizer

Generate synthetic samples

Save synthetic CSV

Evaluate statistical similarity

Evaluate ML utility

Evaluation Strategy
Statistical Evaluation

Distribution comparison plots

KDE overlays for numerical features

Bar plots for categorical variables

Correlation heatmap comparison

Machine Learning Utility

Task: Predict HOSPITAL_EXPIRE_FLAG

Procedure:

Train RandomForest on real dataset

Train RandomForest on synthetic dataset

Compare accuracy

Result from research 

Synthetic Data Generation in He…

:

Training Data	Accuracy
Real Data	86%
Synthetic Data	84%

Small performance gap confirms retained predictive utility.

Full Dataset Extension

Unlike many studies limited to a single table, this repository extends synthetic modeling to:

Clinical diagnoses tables

CPT procedure tables

Laboratory events

Microbiology events

Transfers and services

Patient demographics

Each table follows a standardized pipeline architecture, making the framework modular and reusable.

Repository Structure
.
├── 1. Admissions.ipynb
├── 2. Patient_Table.ipynb
├── 10. D_CPT.ipynb
├── 11. D_ICD_DIAGNOSES.ipynb
├── 12. D_ICD_PROCEDURES.ipynb
├── 13. D_ITEMS.ipynb
├── 14. D_LABITEMS.ipynb
├── 15. ICUSTAYS.ipynb
├── ...
├── Synthetic Data Generation in Healthcare.pdf
├── README.md
└── requirements.txt

Each notebook implements:

Table specific preprocessing

TVAE training

Synthetic sampling

Evaluation

Technologies Used

Python

Pandas

NumPy

Scikit learn

SDV

Matplotlib

Seaborn

Jupyter Notebook

Why This Project Matters

This work demonstrates that:

Synthetic healthcare data can preserve statistical integrity

Machine learning models trained on synthetic data remain competitive

Privacy compliant ML experimentation is achievable

Tabular VAEs are practical for large structured clinical datasets

This creates strong foundations for:

Federated learning

Differential privacy integration

Secure healthcare AI research

Reproducible ML experimentation

Future Directions

Multi table relational synthesis

Differential privacy noise injection

Federated synthetic data training

Transformer based tabular models

Benchmarking against MIMIC IV

Synthetic data risk evaluation

Academic Context

Developed as part of graduate research in Machine Learning and Data Mining at California State Polytechnic University, Pomona.

Co authored research paper:
Synthetic Data Generation for Healthcare 

This repository is for research and academic purposes.

MIMIC III data usage requires credentialed PhysioNet access and compliance with data use agreements.
