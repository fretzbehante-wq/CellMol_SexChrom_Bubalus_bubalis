
# Galaxy Workflow Documentation: Sex-Chromosome Dosage Analysis

**Species:** *Bubalus bubalis* (Water Buffalo/Carabao)  
**Laboratory:** Cell and Molecular Biology  
**Analysis:** Sex-Chromosome Dosage Using NCBI, Galaxy, and R

This directory documents the step-by-step bioinformatics workflow used to retrieve whole-genome sequencing data, assess read quality, align sequencing reads, and calculate chromosome coverage statistics for *Bubalus bubalis* (WGS run `SRR27345303`).

The screenshots provide evidence of the procedures performed in Galaxy.

## Step-by-Step Galaxy Process

### 1. Reference Genome and Data Retrieval

- Selected *Bubalus bubalis*, a diploid mammalian species with an XX/XY sex-chromosome system.
- Retrieved the chromosome-level reference genome from NCBI.
- **Reference assembly:** `GCF_019923935.1`
- **Assembly name:** NDDB_SH_1
- Downloaded the genomic FASTA file and sequence report.
- Verified chromosome identifiers using the NCBI assembly sequence report.
- Identified the X chromosome as `NC_059181.1`.
- Retrieved paired-end whole-genome shotgun (WGS) sequencing reads from NCBI SRA.
- **WGS accession:** `SRR27345303`
- Imported the reference FASTA into Galaxy.
- Imported WGS reads using the Galaxy SRA fasterq-dump tool.

### 2. Quality Control

- Performed FastQC analysis on both forward and reverse sequencing reads.
- Examined per-base sequence quality, GC content, adapter content, and other quality indicators.
- The forward reads showed a warning for GC content and a failure for per-base sequence content.
- The reverse reads showed a warning for GC content.
- Most remaining quality indicators passed.
- Proceeded with alignment without additional trimming because the available quality reports did not indicate a clear need for trimming.

### 3. Read Alignment Using BWA-MEM

- Used **BWA-MEM** to align paired-end WGS reads against the selected reference genome.
- Selected the reference genome from Galaxy history rather than a built-in reference.
- **Reference FASTA:** `GCF_019923935.1_NDDB_SH_1_genomic.fna`
- **Forward reads:** `SRR27345303:forward`
- **Reverse reads:** `SRR27345303:reverse`
- Selected paired-end alignment mode.
- Generated a BAM alignment file.

**Galaxy dataset:** `23: Map with BWA-MEM on dataset 1, 14, and 15`

### 4. BAM Sorting

- Used **Samtools sort** to organize aligned reads by genomic coordinates.
- Selected the BWA-MEM BAM output as input.
- Set the primary sort key to `coordinate`.
- Verified the coordinate-sorted BAM header (`SO:coordinate`).

**Galaxy dataset:** `25: Samtools sort on dataset 23`

### 5. Chromosome Coverage Calculation

- Used **Samtools coverage** on the coordinate-sorted BAM file.
- Selected tabular output instead of histogram output.
- Configured the following parameters:

| Parameter | Setting |
|---|---|
| Pool BAM files | No |
| Input BAM | Dataset 25 |
| Minimum read length | 0 |
| Minimum mapping quality | 20 |
| Minimum base quality | 20 |
| Output format | Tabular |
| Excluded read flags | Default settings |

- Generated chromosome-level coverage statistics.
- Confirmed that the output included the `rname` and `meandepth` columns.
- Downloaded the coverage table as `chromosome_coverage.tsv`.

**Galaxy dataset:** `27: Samtools coverage on dataset 25`

### 6. Chromosome Selection for R Analysis

- Selected five annotated autosomes as the normalization reference.
- Identified the X chromosome using the NCBI sequence report.
- Created `chromosome_groups.csv` with the following labels:

| Chromosome | Reference accession | Group |
|---|---|---|
| Autosome 1 | NC_059157.1 | A |
| Autosome 2 | NC_059158.1 | A |
| Autosome 3 | NC_059159.1 | A |
| Autosome 4 | NC_059160.1 | A |
| Autosome 5 | NC_059161.1 | A |
| X chromosome | NC_059181.1 | X |

- Excluded mitochondrial DNA and other non-target sequences from the normalization analysis.
- Prepared both input files for downstream R analysis.


## Galaxy Workflow / History Link

**Galaxy History:** https://galaxy-main.usegalaxy.org/u/ivan_behante/h/sex-dosage-carabao 


## Notes

- The reference assembly and WGS reads originated from different BioSamples.
- The sex-chromosome dosage result therefore refers to the individual represented by the WGS sequencing reads.
- The resulting X:A ratio suggested an XY-like dosage pattern, but the final interpretation was inconclusive because of very low autosomal sequencing depth.
- Original large FASTA, FASTQ, and BAM files were retained outside GitHub.

## References

1. [NCBI Genome Assembly — GCF_019923935.1](https://www.ncbi.nlm.nih.gov/datasets/genome/GCF_019923935.1/)
2. [NCBI SRA — SRR27345303](https://www.ncbi.nlm.nih.gov/sra/?term=SRR27345303)
3. [Galaxy](https://usegalaxy.org/)
