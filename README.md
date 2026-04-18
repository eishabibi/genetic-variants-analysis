# 🧬 Genetic Variants Clinical Genomics Analysis

**Beginner-friendly step-by-step bioinformatics assignment**  
*Three genetic disorders analysed using ClinVar, OMIM, UCSC Genome Browser, and ACMG/AMP guidelines*

---

## 📋 Table of Contents

1. [Overview](#overview)
2. [Selected Diseases & Variants](#selected-diseases--variants)
3. [Repository Structure](#repository-structure)
4. [Step-by-Step Reproduction Guide](#step-by-step-reproduction-guide)
   - [Step 1: ClinVar Variant Selection](#step-1-clinvar-variant-selection)
   - [Step 2: OMIM Phenotype Lookup](#step-2-omim-phenotype-lookup)
   - [Step 3: UCSC Genome Browser (AlphaMissense & REVEL)](#step-3-ucsc-genome-browser)
   - [Step 4: ACMG/AMP Classification](#step-4-acmgamp-classification)
   - [Step 5: Create the VCF File](#step-5-create-the-vcf-file)
   - [Step 6: Submit VCF to ClinVar for Annotation](#step-6-submit-vcf-to-clinvar-for-annotation)
   - [Step 7: Reproduce the Excel Report](#step-7-reproduce-the-excel-report)
5. [Detailed Variant Notes](#detailed-variant-notes)
6. [Key Databases & Resources](#key-databases--resources)
7. [Prerequisites](#prerequisites)
8. [Citation & References](#citation--references)

---

## Overview

This project performs a clinical genomic analysis of three well-characterised genetic disorders. For each disorder, we:

- Identify the most clinically relevant variant from **ClinVar**
- Describe the variant's functional impact using published literature
- Retrieve phenotype data from **OMIM**
- Visualise pathogenicity scores in the **UCSC Genome Browser** (AlphaMissense + REVEL)
- Apply **ACMG/AMP 2015** classification criteria
- Package all variants into a clinical **VCF file** (GRCh38)
- Submit the VCF to **ClinVar** for automated annotation

---

## Selected Diseases & Variants

| # | Disease | Gene | Variant | ClinVar ID | Significance |
|---|---------|------|---------|------------|--------------|
| 1 | Cystic Fibrosis | CFTR | p.Phe508del (c.1521_1523del) | [7105](https://www.ncbi.nlm.nih.gov/clinvar/variation/7105/) | Pathogenic  |
| 2 | Sickle Cell Disease | HBB | p.Glu6Val (c.20A>T) | [15126](https://www.ncbi.nlm.nih.gov/clinvar/variation/15126/) | Pathogenic  |
| 3 | Huntington Disease | HTT | CAG repeat expansion (≥40 repeats) | [9496](https://www.ncbi.nlm.nih.gov/clinvar/variation/9496/) | Pathogenic  |

---

## Repository Structure

```
genetic-variants-analysis/
│
├── README.md                        ← You are here
├── Genetic_Variants_Analysis.xlsx   ← Main Excel report (5 sheets)
├── patient_variants.vcf             ← Clinical VCF file (GRCh38)
├── genetic_variants.py              ← Python script to regenerate Excel
│
├── screenshots/                     ← UCSC Genome Browser screenshots
│   ├── CFTR_F508del_UCSC.png
│   ├── HBB_Glu6Val_AlphaMissense_REVEL.png
│   └── HTT_CAG_repeat_UCSC.png
│
└── references/
    └── key_papers.md                ← Annotated bibliography
```



---

### Step 1: ClinVar Variant Selection

**What is ClinVar?**  
ClinVar is a free, public database maintained by NCBI (National Center for Biotechnology Information). It stores information about genetic variants and their relationship to human health.

**How to find a variant:**

1. Go to [https://www.ncbi.nlm.nih.gov/clinvar/](https://www.ncbi.nlm.nih.gov/clinvar/)
2. In the search bar, type the gene name (e.g., `CFTR`) and press Enter
3. Filter by **Clinical Significance = Pathogenic** on the left sidebar
4. Look for variants with **4 or 5 review stars** (these are the most trusted)
5. Click on a variant to open its detail page

**For each of our three variants, go directly to:**

| Disease | Direct ClinVar Link |
|---------|---------------------|
| CF – CFTR F508del | https://www.ncbi.nlm.nih.gov/clinvar/variation/7105/ |
| SCD – HBB Glu6Val | https://www.ncbi.nlm.nih.gov/clinvar/variation/15126/ |
| HD – HTT CAG expansion | https://www.ncbi.nlm.nih.gov/clinvar/variation/9496/ |

**What to record from each ClinVar page:**
- Variation ID (number in the URL)
- Gene name, chromosome, position (GRCh38)
- HGVS notation (looks like: `NM_000492.4:c.1521_1523del`)
- Clinical significance & review status (stars)
- Conditions listed
- Submitter comments and citations

---

### Step 2: OMIM Phenotype Lookup

**What is OMIM?**  
OMIM (Online Mendelian Inheritance in Man) is the authoritative catalogue of genetic disorders. Every disease has a MIM number.

**How to use OMIM:**

1. Go to [https://www.omim.org/](https://www.omim.org/)
2. Search for the disease name (e.g., `Cystic Fibrosis`)
3. Click the phenotype entry (phenotype entries start with `#`)
4. Read the **Clinical Synopsis** and **Description** sections
5. Note: Gene entries start with `*`; phenotype entries start with `#`

**Our OMIM entries:**

| Disease | Phenotype MIM | Gene MIM | OMIM URL |
|---------|--------------|----------|----------|
| Cystic Fibrosis | 219700 | 602421 | https://www.omim.org/entry/219700 |
| Sickle Cell Disease | 603903 | 141900 | https://www.omim.org/entry/603903 |
| Huntington Disease | 143100 | 613004 | https://www.omim.org/entry/143100 |

**What to record:**
- Inheritance pattern (AR/AD/XL)
- Clinical features list
- Molecular basis section
- Associated allelic variants

---

### Step 3: UCSC Genome Browser

**What is the UCSC Genome Browser?**  
A web-based tool to visually explore the human genome and see annotations like pathogenicity scores, conservation, and gene structures.

**How to view AlphaMissense and REVEL scores:**

1. Go to [https://genome.ucsc.edu/](https://genome.ucsc.edu/)
2. Click **"Genome Browser"** → select **Human (GRCh38/hg38)**
3. In the search box, paste a genomic coordinate:
   - CF: `chr7:117,559,580-117,559,610`
   - SCD: `chr11:5,226,990-5,227,015`
   - HD: `chr4:3,074,680-3,075,100`
4. Press **Go**

**To add AlphaMissense track:**
- Scroll down to **"Variation and Repeats"** section
- Find **"AlphaMissense"** → set to **"Full"** → click **Refresh**

**To add REVEL track:**
- In the Genome Browser, click **"Add Custom Track"**
- Or search under **Variation → Non-coding Variants** section
- REVEL is available under **"REVEL"** in the track list

**How to take a screenshot:**
- Once you can see the coloured tracks, press **Ctrl+Shift+S** (Windows) or **Cmd+Shift+4** (Mac)
- Or use the browser's built-in **PDF/PS** export: click **"View" → "PDF/PS"**

**Understanding the colour coding:**
- 🔴 **Red = Pathogenic/Likely Pathogenic** (score close to 1.0)
- 🟡 **Yellow = Uncertain significance** (score ~0.5)
- 🟢 **Green = Benign** (score close to 0)

**Note for HTT (Huntington):**
- AlphaMissense and REVEL do NOT score repeat expansions
- Instead, look at the **RepeatMasker** and **STR** (short tandem repeat) tracks
- The CAG repeat region will appear as a repeated sequence block

---

### Step 4: ACMG/AMP Classification

**What is ACMG/AMP?**  
The American College of Medical Genetics and the Association for Molecular Pathology published guidelines in 2015 for classifying genetic variants. Every clinical lab follows these rules.

**The 5 classifications:**
1. **Pathogenic** – causes disease
2. **Likely Pathogenic** – probably causes disease (>90% certainty)
3. **Variant of Uncertain Significance (VUS)** – unknown impact
4. **Likely Benign** – probably harmless
5. **Benign** – harmless

**Key criteria (simplified):**

| Code | Name | Strength | What it means |
|------|------|----------|---------------|
| PVS1 | Null variant | Very Strong | Gene stops working completely |
| PS1 | Same AA change | Strong | Exact change seen before in patients |
| PS3 | Functional studies | Strong | Lab experiments prove it's harmful |
| PS4 | Higher frequency in patients | Strong | More common in sick than healthy people |
| PM1 | Critical domain | Moderate | Change is in an important protein region |
| PM2 | Absent from populations | Moderate | Not found in healthy people |
| PP3 | Computational evidence | Supporting | Computer programs predict pathogenic |
| PP5 | Reputable source | Supporting | Trusted lab or database says it's pathogenic |

**Free tool to apply ACMG criteria:**
- Use **InterVar** online: [https://wintervar.wglab.org/](https://wintervar.wglab.org/)
- Or **Franklin by Genoox**: [https://franklin.genoox.com/](https://franklin.genoox.com/)
- Input your variant's chromosome, position, REF, ALT alleles
- The tool auto-applies ACMG criteria and gives you a classification

---

### Step 5: Create the VCF File

**What is a VCF file?**  
VCF (Variant Call Format) is the standard file format used in genomics to store genetic variants. Think of it as a spreadsheet where each row = one genetic change found in a patient's DNA.

**VCF file structure:**
```
## comment lines (metadata)  ← start with ##
#CHROM  POS  ID  REF  ALT  QUAL  FILTER  INFO  FORMAT  SAMPLE
chr7  117559593  rs113993960  ATCT  A  5000  PASS  Gene=CFTR;...  GT:DP  0/1:120
```

**Column meanings:**
| Column | Meaning | Example |
|--------|---------|---------|
| CHROM | Chromosome | chr7 |
| POS | Position on chromosome | 117559593 |
| ID | Known variant ID | rs113993960 |
| REF | Reference DNA sequence | ATCT |
| ALT | Patient's DNA sequence | A (means 3 bases deleted) |
| QUAL | Quality score (higher = better) | 5000 |
| FILTER | Did variant pass quality check? | PASS |
| INFO | Extra details about variant | Gene=CFTR;ClinSig=Pathogenic |
| FORMAT | What data is in the SAMPLE column | GT:DP:GQ |
| SAMPLE | Patient's actual genotype data | 0/1:120:99 |

**Genotype codes:**
- `0/0` = homozygous reference (patient has normal DNA at this position)
- `0/1` = heterozygous (one normal copy, one mutant copy = carrier or affected for dominant diseases)
- `1/1` = homozygous alternate (both copies have the mutation = affected for recessive diseases)

**Our VCF file explains:**
- SCD patient is **1/1** (homozygous HbSS = has sickle cell disease)
- CF patient is **0/1** (heterozygous = carrier; would need 2nd CFTR variant to have CF)
- HD patient is **0/1** (one mutant HTT allele = affected, as HD is autosomal dominant)

**To view the VCF file:** Open `patient_variants.vcf` in any text editor (Notepad, VS Code, etc.)

---

### Step 6: Submit VCF to ClinVar for Annotation

>  **Important for beginners:** ClinVar has two services that sound similar but are different:
> - **Submitting variants** = telling ClinVar about new data from your lab (requires account + institutional affiliation)
> - **Annotating variants** = asking ClinVar to add clinical information to your existing VCF file

**Method A: ClinVar Variant Annotation (Recommended for beginners)**

ClinVar does not have a one-click "annotate my VCF" button. Instead, use these free annotation tools that pull data FROM ClinVar:

1. **Ensembl VEP (Variant Effect Predictor)** — the most popular tool  
   🔗 https://www.ensembl.org/Tools/VEP  
   - Click **"Launch VEP"**
   - Upload your `patient_variants.vcf` file
   - Select **Human GRCh38**
   - Under **"Additional annotations"**, check ✅ **ClinVar** and ✅ **OMIM**
   - Click **"Run"**
   - Download annotated VCF from results page

2. **ANNOVAR** (command line tool)  
   🔗 https://annovar.openbioinformatics.org/  
   ```bash
   # After installing ANNOVAR:
   perl annotate_variation.pl -buildver hg38 patient_variants.vcf humandb/ \
       -protocol refGene,clinvar_20240101,dbnsfp47a \
       -operation g,f,f -nastring .
   ```

3. **Franklin by Genoox** (web-based, beginner-friendly)  
   🔗 https://franklin.genoox.com/  
   - Create a free account
   - Upload your VCF
   - Automatically annotates with ClinVar, OMIM, gnomAD, AlphaMissense

**Method B: Official ClinVar Submission (Advanced — for labs with patient consent)**

1. Create an NCBI account: https://www.ncbi.nlm.nih.gov/account/
2. Request a ClinVar Submitter ID: https://www.ncbi.nlm.nih.gov/clinvar/docs/submit/
3. Use the ClinVar Submission Portal: https://submit.ncbi.nlm.nih.gov/clinvar/
4. Follow the submission template (Excel format available on the portal)
5. ClinVar staff will review and approve the submission

---

### Step 7: Reproduce the Excel Report

**Prerequisites:**
```bash
pip install openpyxl
```

**Run the script:**
```bash
python genetic_variants.py
```

This will generate `Genetic_Variants_Analysis.xlsx` with 5 sheets:
1. **Summary** — overview table of all 3 variants
2. **CF – CFTR F508del** — full Cystic Fibrosis analysis
3. **SCD – HBB Glu6Val** — full Sickle Cell Disease analysis
4. **HD – HTT CAG Expansion** — full Huntington Disease analysis
5. **ACMG Summary** — side-by-side ACMG criteria comparison
6. **VCF File Guide** — explanation of the VCF format fields

---

## Detailed Variant Notes

### Variant 1: CFTR p.Phe508del (Cystic Fibrosis)
- **Position:** chr7:117,559,593 (GRCh38)
- **Change:** 3-bp deletion (CTT removed) → loss of phenylalanine at codon 508
- **Mechanism:** Protein misfolding → ER retention → proteasomal degradation
- **Frequency:** ~70% of all CF alleles worldwide; ~2–3% carrier rate in Northern Europeans
- **Treatment target:** Elexacaftor/tezacaftor/ivacaftor (Trikafta) corrects misfolding
- **Why chosen:** Most common CF variant globally; best characterised pathogenic CFTR allele

### Variant 2: HBB p.Glu6Val (Sickle Cell Disease)
- **Position:** chr11:5,227,002 (GRCh38)
- **Change:** A>T transversion → glutamic acid → valine at position 6
- **Mechanism:** HbS polymerisation under hypoxia → sickling → vaso-occlusion
- **AlphaMissense:** 0.9941 (nearly maximum score) — likely pathogenic
- **REVEL:** 0.932 — highly pathogenic
- **Why chosen:** Textbook example of a disease-causing missense variant; highest quality pathogenicity scores

### Variant 3: HTT CAG repeat expansion (Huntington Disease)
- **Position:** chr4:3,074,877 (GRCh38)
- **Normal:** ≤26 CAG repeats; **Pathogenic:** ≥40 repeats
- **Patient:** 42 CAG repeats (full penetrance, expected onset ~45 years)
- **Mechanism:** polyQ expansion → mHTT aggregation → striatal neuron death
- **Note:** AlphaMissense and REVEL do NOT apply to repeat expansions — this is expected and correct
- **Why chosen:** Classic example of repeat expansion disease; demonstrates limitations of standard pathogenicity scoring tools

---

## Key Databases & Resources

| Resource | URL | What it does |
|----------|-----|--------------|
| ClinVar | https://www.ncbi.nlm.nih.gov/clinvar/ | Variant-disease relationships |
| OMIM | https://www.omim.org/ | Disease phenotype catalogue |
| UCSC Genome Browser | https://genome.ucsc.edu/ | Genome visualisation |
| gnomAD | https://gnomad.broadinstitute.org/ | Population allele frequencies |
| Ensembl VEP | https://www.ensembl.org/Tools/VEP | Variant annotation |
| Franklin | https://franklin.genoox.com/ | Clinical variant interpretation |
| AlphaMissense | https://alphamissense.hegelab.org/ | AI-based missense pathogenicity |
| InterVar | https://wintervar.wglab.org/ | ACMG/AMP auto-classification |
| CFTR2 | https://cftr2.org/ | CFTR-specific variant database |
| ClinGen | https://clinicalgenome.org/ | Gene-disease validity |

---

## Prerequisites

**Software:**
- Python 3.8+ with `openpyxl` library
- Any text editor (VS Code recommended)
- Web browser (Chrome/Firefox)

**Install Python dependencies:**
```bash
pip install openpyxl
```

**Optional (for advanced analysis):**
```bash
pip install pandas matplotlib seaborn
```

---

## Citation & References

1. Richards, S. et al. (2015). Standards and guidelines for interpretation of sequence variants. *Genet Med*, 17(5):405–424. https://doi.org/10.1038/gim.2015.30

2. Riordan, J.R. et al. (1989). Identification of the cystic fibrosis gene. *Science*, 245(4922):1066–1073.

3. Cheng, S.H. et al. (1990). Defective intracellular transport and processing of CFTR is the molecular basis of most cystic fibrosis. *Cell*, 63(4):827–834.

4. Pauling, L. et al. (1949). Sickle cell anemia, a molecular disease. *Science*, 110(2865):543–548.

5. Ingram, V.M. (1956). A specific chemical difference between globins. *Nature*, 178:792–794.

6. The Huntington's Disease Collaborative Research Group (1993). A novel gene containing a trinucleotide repeat. *Cell*, 72(6):971–983.

7. Tabrizi, S.J. et al. (2019). Targeting Huntingtin Expression in Patients with Huntington's Disease. *NEJM*, 380:2307–2316.

8. Chalmers, Z.R. et al. (2017). Analysis of 100,000 human cancer genomes. *Genome Med*, 9(1):34.

9. Heijerman, H.G.M. et al. (2019). Efficacy and safety of the elexacaftor plus tezacaftor plus ivacaftor combination. *Lancet*, 394(10212):1940–1948.

10. Brnich, S.E. et al. (2020). Recommendations for application of the functional evidence PS3/BS3 criterion using the ACMG/AMP sequence variant interpretation framework. *Genome Med*, 12(1):3.

---

## License

This repository is for educational purposes. All variant data is publicly available from NCBI ClinVar, OMIM, and gnomAD databases.

---

*Created as part of a clinical genomics training assignment. Data sourced from public databases (ClinVar, OMIM, UCSC Genome Browser) as of March 2026.*
