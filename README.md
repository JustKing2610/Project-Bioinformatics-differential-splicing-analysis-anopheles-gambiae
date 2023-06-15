# Alternative splicing analysis of chemosensory genes from antennae and maxillary palps in anopheles colluzzi and quadriannulatus 

An overview of the tools, scripts and commands used to create this pipeline

## Description

In this research we provide alternatively spliced gene variants that may be responsible for the human host preference in An. coluzzii. RNA-seq data generated from the antennae and maxillary palp of both An. coluzzii and An. quadriannulatus by G. Athrey et all. will be used in this research. The main goal of this project is to look into the alternative splicing of genes expressed in the antennae and maxillary palps. By finding certain splice variants which are more present in one of the 2 species analysed, we provide the necessary information to combat the spread of malaria since these alternative splice variants might contribute to the host seeking behaviour. To reach this goal we will use several tools for quality control of the raw RNA-seq data, filtering and trimming the raw data, followed by tools to detect alternative splice events. The tools used for this research are FASTQC, Trimmomatic, TopHat2, StringTie2, Kallisto, Samtools, SUPPA2 and DEseq2. Using these tools, the alternative splicing and differential expression can be detected in the RNA-seq data. 
## Raw data availibity
To gather the raw RNA-seq data follow this link: https://www.ncbi.nlm.nih.gov/sra/?term=PRJNA400609

## Getting Started
To repeat the analysis as described in the paper, a few tools are to be installed into a terminal environment, in this paper we used MobaXterm.
### necessary programs
#### alternative splicing analysis in MobaXterm
The first program needed to be able to repeat the research is python, here we used python (version 2.3)<br />
Fastqc (Version 0.12.1) and multiqc (version 1.14) were used to asses raw and trimmed data quality<br />
Trimmomatic (version 0.39) was used for quality trimming the raw reads.<br />
Tophat (version 2.1.1) was used for mapping the reads to the reference genome cited in the paper<br />
kallisto (version 0.48.0) was used for a psuedo alignment and transcriptome indexing for suppa<br />
suppa python scripts (version 2.3) were installed via conda, following instructions from: https://github.com/comprna/SUPPA

#### Differential gene expression analysis in galaxy
On http://usegalaxy.eu/, the trimmed reads were imported.<br />
RNA star (version 2.7.10) was used to map the reads to the reference genome <br />
RNA star mapped bam files where fed into Featurecounts (version 2.0.3) <br />
The featurecounts table was then fed into DESeq2 (version 2.11.40.7)<br />
Annotation of the DESeq2 results was done with Annotate DESeq2/DEXSeq output tables” (version 1.1.0) <br />

### Different scripts and their purpose/use

#### FastQC
The FastQC script is used to quality check the RNA-seq reads. This has been done before and after trimming with trimmomatic.
#### Trimmomatic
Trimmomatic is used for filtering and trimming the RNA-seq reads. So that the bad reads are filtered out, and less quality read-ends are trimmed of the reads.
#### Tophat
Tophat is used to map the trimmed and filtered reads on the reference genome. This results in .bam files, which can be used for assembly
#### StringTie
For the assembly StringTie is used. This tool generated gtf files for each sample.
#### Suppa
Suppa is a tool to find and measure alternative splicing. This is used for each sample
### Parameters on the command line
#### Trimmomatic
LEADING:28 <br />
TRAILING:28 <br />
SLIDINGWINDOW:10:30 <br />
MINLEN:45 <br />

#### Tophat
read-mismatches: 3 (for 50bp read files) / 7 (for 124bp read files)  <br /> 
read-edit-dist: 6 <br /> 
library-type: fr-unstranded <br /> 
-p: 4 <br />

#### kallisto
--single<br />
-b: 100<br />
-l: 50 <br />
-s: 20<br />

### Parameters in galaxy

#### RNA STAR
Single end reads <br />
use ref genome from history (Anopheles gambiae agamp4 GTF) <br />
Length of the SA pre-indexing string: 14 <br />
build index with gene model <br />
Length of the genomic sequence around annotated junctions: 49  <br />

#### feature counts
Specify strand information: unstranded<br />
gene annotation file: a GFF/GTF from history<br />
GFF feature type filter: exon<br />
GFF gene identifier: gene_id<br />
does input have read pairs: no single end<br />

#### DESeq2 
Select datasets per level<br />
Factor1 : species<br />
Factor levels: Coluzzii and Quadriannulatus<br />


## Authors

Tim van der Wiel
Justin Iking

