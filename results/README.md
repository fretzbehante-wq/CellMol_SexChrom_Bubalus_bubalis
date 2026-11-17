
# Results Directory: Sex-Chromosome Dosage Analysis

This directory contains the output files generated for *Bubalus bubalis* (water buffalo/carabao) following whole-genome sequencing read-depth analysis using Galaxy, Samtools, and R. Chromosome coverage was normalized against the median autosomal depth to evaluate the X-to-autosome (X:A) ratio and infer the sex-chromosome complement of the WGS donor.


## File Descriptions

- **`sex_inference.txt`** — Summary text containing the calculated median autosomal depth, X:A ratio, Y:A ratio (if available), and final dosage interpretation.

- **`chromosome_relative_depth.csv`** — Tabular results containing chromosome identifiers (`rname`), assigned chromosome groups (`A` or `X`), mean read depth (`meandepth`), and normalized relative depth (`relative_depth`).

- **`chromosome_depth.png`** — Bar plot showing normalized read-depth ratios for five selected autosomes and one X chromosome, with reference lines at 0.5 and 1.0.


## Summary Results

| Parameter | Result |
|---|---|
| Species | *Bubalus bubalis* |
| Reference assembly | GCF_019923935.1 |
| WGS accession | SRR27345303 |
| Sex-chromosome system | XX/XY |
| Autosomes analyzed | 5 |
| Sex chromosome analyzed | X |
| Median autosomal depth (A) | 0.722326 |
| X chromosome mean depth | Approximately 0.450 |
| X:A ratio | Approximately 0.622 |
| Y:A ratio | NA |
| Preliminary dosage pattern | XY-like |
| Final interpretation | Inconclusive: very low autosomal depth |


## Interpretation

The calculated X:A ratio of approximately **0.622** is within the XY-like range defined by the laboratory analysis script. However, the median autosomal depth was only **0.722326**, which is below the minimum depth threshold of 1.

Therefore, the final result was classified as **"Inconclusive: very low autosomal depth."**

Although the observed ratio suggests an XY-like dosage pattern and the WGS donor was recorded as male, the low sequencing depth limits confidence in the inferred sex-chromosome complement.

The result refers specifically to the WGS donor because the reference genome assembly and sequencing reads originated from different BioSamples.


