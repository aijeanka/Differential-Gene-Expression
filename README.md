# **Colorectal Cancer Relapse and Recurrence Analysis**

## **Project Overview**

This repository contains the results and documentation of a bioinformatics project aimed at identifying differentially expressed genes (DEGs) in patients experiencing relapse and recurrence of colorectal cancer. The analysis compares clinical data and gene expression data to uncover insights into the molecular mechanisms distinguishing these patient groups.

## **Project Objectives**

- Identify DEGs between patients with relapse and those with recurrence of colorectal cancer.
- Ensure alignment between clinical and gene expression data.
- Perform data cleaning and transformation to create a coherent dataset for analysis.

## **Methodology**

### **1. Clinical Data Subsetting**

- **Objective**: Create a subset of clinical data with 20 unique patient IDs for each group (relapse and recurrence).
- **Key Attribute**: `RECURRENCE_ANY` column.

### **2. Gene Expression Data Transformation**

- **Objective**: Transpose gene expression data from log2 scale to align with clinical data.
- **Initial State**: 80 rows representing different genes.
- **Post-Transformation**: 80 columns corresponding to patients.

### **3. Data Alignment and Sanity Check**

- Ensure alignment between patient IDs in the clinical data and gene expression data.
- Identify and remove extraneous rows or "junk" data to ensure dataset integrity.

### **4. Differential Gene Expression Analysis**

Performed differential gene expression analysis to identify top DEGs distinguishing the two patient groups.

**Key Outputs**:

- **Top 20 Genes (DEGs)**:  
  - `Aizhan-Uteubayeva-TTestHW-05-Top20Genes.tsv`

- **Code for Analysis**:  
  - R Markdown: `Aizhan-Uteubayeva-TTestHW-02-a-Code.Rmd`  
  - HTML Report: `Aizhan-Uteubayeva-TTestHW-02-b-Code.html`

- **Output Data**:  
  - Processed Results: `Aizhan-Uteubayeva-TTestHW-04-Output.csv`

## **Repository Structure**

```
├── data/
│   └── Aizhan-Uteubayeva-TTestHW-05-Top20Genes.tsv
│
├── analysis/
│   ├── Aizhan-Uteubayeva-TTestHW-02-a-Code.Rmd
│   └── Aizhan-Uteubayeva-TTestHW-02-b-Code.html
│
├── results/
│   └── Aizhan-Uteubayeva-TTestHW-04-Output.csv
│
└── README.md
```

## **Skills Demonstrated**

- **Bioinformatics Analysis**: Differential gene expression analysis.
- **Data Cleaning and Transformation**: Ensuring alignment of clinical and gene expression data.
- **Reproducible Research**: Use of R Markdown for documenting analysis workflows.
- **Data Visualization**: Generating HTML reports and summarizing results.

## **Author**

**Aizhan Uteubayeva**

## **License**

This project is licensed under the MIT License.
