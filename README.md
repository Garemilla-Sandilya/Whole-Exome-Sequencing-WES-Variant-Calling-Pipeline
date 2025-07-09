# Whole Exome Sequencing (WES) Variant Calling Pipeline

This project showcases a complete **Whole Exome Sequencing (WES)** pipeline for variant calling and annotation using public Illumina paired-end exome data from NCBI SRA.

---

## 🧬 Pipeline Overview

### 🟢 Step 1: Data Retrieval
- Downloaded data using **SRA Toolkit** (`prefetch` and `fastq-dump`)
- Example dataset: `SRR8879056`

### 🧪 Step 2: Quality Control
- Evaluated raw and trimmed reads using [FastQC](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/)
- Removed adapters and low-quality bases with [Trimmomatic](http://www.usadellab.org/cms/?page=trimmomatic)

### 🧬 Step 3: Alignment
- Downloaded and indexed **hg38** reference genome
- Aligned reads using [BWA](https://github.com/lh3/bwa)
- Converted and sorted SAM to BAM using **SAMtools**

### 🧹 Step 4: Post-processing
- Added Read Groups using **GATK AddOrReplaceReadGroups**
- Marked PCR duplicates with **GATK MarkDuplicates**
- Recalibrated base quality scores using **BQSR**

### 🔍 Step 5: Variant Calling
- Called variants with **GATK HaplotypeCaller**
- Separated SNPs and INDELs using **GATK SelectVariants**
- Applied filters using **GATK VariantFiltration**
- Merged high-confidence variants using **GATK MergeVcfs**
- Retained only `PASS` variants using **bcftools**

### 🧬 Step 6: Variant Annotation
- Annotated variants with [Ensembl VEP](https://www.ensembl.org/info/docs/tools/vep/index.html)
- Used VEP filters to retain only **canonical** and **protein-coding** variants
- Formatted VEP output into a clean, tab-delimited report for downstream analysis

---

## 📂 Key Tools & Dependencies

| Tool        | Role                                 |
|-------------|--------------------------------------|
| FastQC      | Quality control                      |
| Trimmomatic | Adapter trimming                     |
| BWA         | Sequence alignment                   |
| SAMtools    | File conversion and sorting          |
| GATK        | Variant calling, BQSR, filtering     |
| VEP         | Variant annotation                   |
| bcftools    | Filtering variants                   |
| awk/sed     | VCF formatting & cleanup             |

---

## 📦 Output Files

- `Sample_aligned_sorted.bam`: Cleaned aligned reads
- `Sample_raw_variants.vcf`: Raw variant calls
- `Sample_filtered_all.vcf`: Filtered SNPs & INDELs
- `Sample_PASS.vcf`: Variants with PASS status
- `Sample.vep.vcf`: VEP-annotated variants
- `Sample.vep.f.txt`: Final annotated, formatted variant table

---
