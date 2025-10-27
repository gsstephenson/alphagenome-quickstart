# AlphaGenome Quick Start Notebook

This notebook provides a comprehensive introduction to using AlphaGenome, a deep learning model that predicts functional genomic outputs from DNA sequences.

## Overview

AlphaGenome enables researchers to:
- Predict epigenomic assay outputs (DNase, CAGE, RNA-seq) from DNA sequences
- Analyze variant effects on gene expression and regulation
- Perform in silico mutagenesis to identify important regulatory elements
- Generate tissue-specific predictions across hundreds of cell types

## Setup

### Prerequisites

- Python 3.11+
- Conda environment manager
- AlphaGenome API key

### Installation

1. **Activate the conda environment:**
   ```bash
   conda activate alphagenome-env
   ```

2. **Install dependencies:**
   ```bash
   pip install alphagenome python-dotenv matplotlib pandas jupyterlab ipython
   ```

3. **Configure API key:**
   Create a `.env` file in this directory with your AlphaGenome API key:
   ```
   ALPHA_GENOME_KEY=your_api_key_here
   ```

### Running the Notebook

Start Jupyter Lab:
```bash
jupyter lab quick_start.ipynb
```

Or open directly in VS Code with the Jupyter extension.

## Notebook Contents

### 1. Setup & Authentication
- Securely loads API key from `.env` file
- Initializes the AlphaGenome DNA model client

### 2. Basic DNA Sequence Prediction
**Demonstrates:** Making predictions from a simple DNA sequence

- Input: Short DNA sequence ("GATTACA") padded to 1 Mbp
- Output: DNase hypersensitivity predictions for lung tissue
- Result: Base-pair resolution predictions (1,048,576 positions)

### 3. Multi-Assay & Multi-Tissue Predictions
**Shows:** Requesting multiple assay types and tissues simultaneously

- Assays: CAGE (Cap Analysis of Gene Expression) and DNase
- Tissues: Brain and lung
- Output includes strand-specific predictions and metadata

### 4. Genome Interval Analysis
**Analyzes:** Real genomic regions with gene annotations

- Loads GENCODE gene annotations (hg38)
- Extracts interval around *CYP2B6* gene (chr19)
- Predicts RNA-seq expression for liver tissue
- Visualizes transcript structures with expression tracks

### 5. Variant Effect Prediction
**Evaluates:** How genetic variants affect gene regulation

- Creates variant: chr22:36201698 A→C
- Predicts RNA-seq changes in colon tissue
- Visualizes reference vs alternate allele predictions
- Shows impact on nearby gene *APOL4*

### 6. Gene-Level Variant Scoring
**Quantifies:** Variant impact across genes and tissues

- Uses recommended RNA-seq variant scorer
- Aggregates predictions into gene-level scores
- Output: 37 genes × 667 tissue conditions
- Identifies affected genes: RBFOX2, APOL4, APOL1, MYH9, TXN2, etc.

### 7. In Silico Mutagenesis (ISM)
**Discovers:** Important regulatory sequences

- Tests all single-base substitutions in a 256 bp window
- Runs 768 variants (256 positions × 3 alternates each)
- Scores DNase accessibility changes
- Generates sequence logo showing critical nucleotides
- Reveals regulatory motifs in the sequence

## Key Features Demonstrated

✅ **Multi-scale analysis**: Sequence → tracks → gene scores  
✅ **Multiple assay types**: DNase, CAGE, RNA-seq  
✅ **Tissue specificity**: Organ-specific predictions  
✅ **Variant interpretation**: Quantitative effect scoring  
✅ **Regulatory discovery**: Motif identification via ISM  
✅ **Production-ready**: Real coordinates, standardized ontologies

## Output Types

- **DNase-seq**: Chromatin accessibility
- **CAGE**: Transcription start site activity
- **RNA-seq**: Gene expression levels

All predictions are tissue/cell-type specific using UBERON and EFO ontology terms.

## Data Formats

- **Input**: DNA sequences, genomic intervals (Interval objects), variants (Variant objects)
- **Output**: NumPy arrays for tracks, AnnData objects for gene scores, pandas DataFrames for metadata
- **Annotations**: GENCODE GTF format (Feather files for fast loading)

## Use Cases

This workflow is ideal for:
- **Variant interpretation**: Understanding non-coding variant effects
- **Regulatory genomics**: Identifying enhancers and promoters
- **Gene expression modeling**: Predicting tissue-specific expression
- **Synthetic biology**: Designing regulatory elements
- **Genome engineering**: Optimizing CRISPR target sites

## Tips

- Use appropriate sequence lengths: 1 Mbp (1,048,576 bp) or 2 Kbp (2,048 bp)
- Ontology terms follow UBERON (tissues/organs) and EFO (cell types) standards
- Large predictions are memory-intensive; consider batch processing
- ISM is computationally expensive; use focused windows (≤512 bp)
- Variant scores aggregate across multiple quantiles and tissues

## Resources

- [AlphaGenome Documentation](https://github.com/google-deepmind/alphagenome)
- [GENCODE Annotations](https://www.gencodegenes.org/)
- [UBERON Ontology](http://uberon.github.io/)
- [EFO Ontology](https://www.ebi.ac.uk/efo/)

## Troubleshooting

**API Key Issues:**
- Ensure `.env` file is in the same directory as the notebook
- Check that the key is valid and not expired

**Memory Errors:**
- Reduce the number of requested tissues/assays
- Use smaller genomic intervals
- Process variants in batches

**Slow Performance:**
- First predictions are slower due to model loading
- Use batch API calls when possible
- Consider local caching for repeated predictions

## License

This notebook uses the AlphaGenome API. Check the [AlphaGenome license](https://github.com/google-deepmind/alphagenome) for usage terms.

## Citation

If you use AlphaGenome in your research, please cite the appropriate publications from the AlphaGenome project.

---

**Last Updated:** October 26, 2025
