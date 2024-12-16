# **Colorectal Cancer Relapse and Recurrence Analysis**

## **Project Overview**

This repository contains data, code, and results for a bioinformatics study aimed at identifying differentially expressed genes (DEGs) between patients experiencing relapse and those who did not. The analysis integrates clinical data and gene expression data, applies statistical testing (T-tests), and identifies significant genes associated with colorectal cancer relapse.

---

## **Highlights**

- **Packages Used**:  
  - `tidyverse` – Data manipulation and visualization  
  - `limma` – Differential gene expression analysis  
  - `knitr` – Dynamic report generation  
  - `dplyr` – Data wrangling  
  - `ggplot2` – Data visualization  
  - `readr` – Reading and writing CSV/TSV files  

- **Code**:  
  R Markdown script for differential gene expression analysis and data preparation.

- **Reproduced Figures**:  
  - Top 20 differentially expressed genes  
  - T-test results sorted by p-values  

---

## **Repository Organization**

For improved reproducibility and clarity, the repository is organized as follows:

```
Colorectal_Cancer_Analysis/
│
├── data/                        # Raw and processed data files
│   ├── CRC_PILOT_clinical_data_HIDS.tsv
│   ├── CRC_PILOT_withGeneAnno.tsv
│   └── output/                  # Outputs from sanity checks and analysis
│       ├── CRC_ClinBaseIDs.tsv
│       ├── CRC_ClinCompIDs.tsv
│       ├── CRC_GeneExpBaseIDs.tsv
│       ├── CRC_GeneExpCompIDs.tsv
│       └── CRCgenExpFeatureIDsCheck.tsv
│
├── scripts/                     # Analysis scripts and functions
│   ├── Aizhan-Uteubayeva-TTestHW-02-a-Code.Rmd
│   ├── Aizhan-Uteubayeva-TTestHW-02-b-Code.html
│   └── fnTTest.R                # Custom T-test function
│
├── results/                     # Results and final output files
│   ├── CRC_TTest.csv
│   ├── p_final.csv
│   └── final_features.csv
│
└── README.md                    # Project documentation
```

---

## **Methodology**

### **Step 1: Data Import**

- **Clinical Data**: `CRC_PILOT_clinical_data_HIDS.tsv`  
  - Contains patient IDs and outcome information (relapse or no relapse).  
- **Gene Expression Data**: `CRC_PILOT_withGeneAnno.tsv`  
  - Log2-normalized gene expression data with gene annotations.

**Code Example**:
```r
c.clinData <- read.table("CRC_PILOT_clinical_data_HIDS.tsv", sep="\t", header=TRUE, stringsAsFactors=FALSE)
c.geneExp <- read.table("CRC_PILOT_withGeneAnno.tsv", sep="\t", header=TRUE, stringsAsFactors=FALSE, row.names=1)
```

### **Step 2: Data Cleaning and Transformation**

- **Transpose Gene Expression Data**:  
  Gene expression data is transposed to align patients as columns and genes as rows.

- **Filter Tumor Samples**:  
  Exclude normal samples from the gene expression data.  
  ```r
  c.geneExp2 <- c.geneExp %>% select(-contains("Normal"))
  ```

- **Extract Cleaned Sample IDs**:  
  Clean sample IDs to match clinical data using a custom function `funSplit()`.  
  ```r
  colnames(c.geneExp2) <- apply(as.matrix(colnames(c.geneExp2)), 1, funSplit)
  ```

### **Step 3: Align Clinical and Gene Expression Data**

- Ensure that the sample IDs in the clinical data match those in the gene expression data.  
- Subset gene expression data to include only the 40 patients of interest (20 relapse, 20 no relapse).

**Outputs**:  
- `output/CRC_ClinBaseIDs.tsv`: Baseline patient IDs  
- `output/CRC_ClinCompIDs.tsv`: Comparison patient IDs  
- `output/CRC_GeneExpBaseIDs.tsv`: Gene expression IDs for baseline group  
- `output/CRC_GeneExpCompIDs.tsv`: Gene expression IDs for comparison group  

### **Step 4: Differential Gene Expression Analysis (T-test)**

- Perform T-tests to identify differentially expressed genes between the baseline and comparison groups using the custom `fnTTest` function.  

**Function Call**:  
```r
results1 <- fnTTest(baseGroup=c.geneExpTumorBase, compGroup=c.geneExpTumorComp,
                    testName="CRC_TTest_", baseGroupName="Non-relapsed",
                    compGroupName="Relapsed", folderName="output")
```

**Output**:  
- `CRC_TTest.csv`: Full T-test results with p-values and fold changes.

### **Step 5: Extract Significant Genes**

- Extract genes with a p-value < 0.01 and create an ordered list of significant genes.  
- Select the top 20 differentially expressed genes.

**Outputs**:  
- `results/p_final.csv`: Genes with p-value < 0.01, ordered by p-value.  
- `results/final_features.csv`: Top 20 differentially expressed genes.

**Code Example**:  
```r
p <- c.ttest[c.ttest$Pvalue < 0.01, ]
p_final <- p[order(p$Pvalue), ]
write_csv(p_final, "results/p_final.csv")

final_features <- head(p_final, 20)
write_csv(final_features, "results/final_features.csv")
```

---

## **Steps to Reproduce the Analysis**

1. **Set Up Environment**:  
   Install the required R packages:  
   ```r
   install.packages(c("tidyverse", "limma", "knitr", "dplyr", "readr"))
   ```

2. **Clone the Repository**:  
   ```bash
   git clone https://github.com/yourusername/Colorectal_Cancer_Analysis.git
   cd Colorectal_Cancer_Analysis
   ```

3. **Prepare Data**:  
   Ensure the clinical and gene expression data files are in the `data/` directory.

4. **Run the Analysis**:  
   Execute the R Markdown script:  
   ```r
   rmarkdown::render("scripts/Aizhan-Uteubayeva-TTestHW-02-a-Code.Rmd")
   ```

5. **Review Results**:  
   - HTML Report: `scripts/Aizhan-Uteubayeva-TTestHW-02-b-Code.html`  
   - Significant Genes: `results/p_final.csv` and `results/final_features.csv`

---

## **Skills Demonstrated**

- **Bioinformatics Analysis**: Differential gene expression and statistical testing.  
- **Data Cleaning**: Filtering and aligning clinical and gene expression data.  
- **Reproducible Research**: Using R Markdown and custom functions.  
- **Data Visualization**: Generating reports and visual summaries.

---

## **Author**

**Aizhan Uteubayeva**

---

## **License**

This project is licensed under the **MIT License**. See the `LICENSE` file for details.
