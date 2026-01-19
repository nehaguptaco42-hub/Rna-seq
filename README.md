# Rna-seq
notes regarding ngs analysis jan26

#Workflow used for rna seq analysis using galaxy

1.Download files from For data download:
https://zenodo.org/records/4249555 [SRR1552444, SRR1552445, SRR1552446, SRR1552447]

2.open galaxy https://usegalaxy.org/

3.upload the following files SRR1552444, SRR1552445, SRR1552446, SRR1552447

4.go to tools and select FASTQ read quality reports

5.Ran FastQC for quality control analysis

6.Observed quality metrics such as per-base sequence quality, GC content, and adapter content

7.Go to tools and run trim gallore

8. Run bowtie2

9. run feature counts

10. run deseq2

# FASTQC result ( SRR1552447)

1.per base sequence quality

![Screenshot 2026-01-19 175145](https://github.com/user-attachments/assets/4e28838e-fd16-48b9-8f29-6a13bc627c0e)

2.Overrepresented sequences

![Screenshot 2026-01-19 175301](https://github.com/user-attachments/assets/52e5621b-65cf-44cb-ad4f-0b6376d634fa)

3.Adaptor content

![Screenshot 2026-01-19 175338](https://github.com/user-attachments/assets/16bc0807-bd62-4da0-8888-0d987e5489bf)


# Observation
Reads are good initially but 3' end trimming is recommended before downstream analysis


# Trim gallore
it trims low quality 3' ends and adapters,improving read quality some reads may become shorter or removed.after trimming the overall read quality improves.

# Bowtie2

bowtie2 is a fast aligner used to map trimmed sequencing reads to a reference genome after quality controlHigh-quality trimmed reads were aligned to the reference genome using Bowtie2.

![Screenshot 2026-01-19 182051](https://github.com/user-attachments/assets/ec5e5164-3e2c-43d4-a624-c67df020d740)


# Feature counts

it is used to convert reads mapped to genes from aligned BAM files for downstream expression analysis

![Screenshot 2026-01-19 182112](https://github.com/user-attachments/assets/9ff5f17e-5cb8-48fb-b868-a137c2d3a173)


# deseq2
it is used to analyze differential genes expression by comparing read counts between conditions

![Screenshot 2026-01-19 182816](https://github.com/user-attachments/assets/e0ceb5e8-31c6-4de0-a688-5ca4e3e3e3da)


![Screenshot 2026-01-19 182928](https://github.com/user-attachments/assets/8b48beca-5f29-4600-8149-2136f8d08113)
![Screenshot 2026-01-19 183258](https://github.com/user-attachments/assets/7d43d695-2ae5-4666-9ce1-a199e265f3ee)


# Heatmap Analysis
After differential expression analysis using DESeq2, a heatmap was generated from the normalized expression matrix.

The heatmap visualizes gene expression patterns across samples.

Rows represent genes (often top differentially expressed genes).

Columns represent samples or conditions.

Color intensity indicates relative expression levels (e.g., high vs low expression).

Clustering helps identify: Similar expression profiles between samples. Groups of co-regulated genes













# Learned about
# PCR (Polymerase Chain Reaction)
PCR is a technique used to amplify DNA, producing millions of copies of a specific DNA sequence.

Enzyme Used in PCR: Taq DNA polymerase, Thermostable enzyme, Isolated from Thermus aquaticus.

Steps of PCR: Denaturation (94–95°C)- Double-stranded DNA separates into single strands Annealing (50–65°C)- Primers bind to complementary DNA sequences Extension / Elongation (72°C)- Taq polymerase synthesizes new DNA strands

Primers in PCR: Short DNA sequences (18–25 bp). Define the region to be amplified. Proper primer design is essential for specificity.

Primers cannot be designed for any reaction without sequence information. Design depends on Tm, GC content, and specificity. Tools such as NCBI Primer-BLAST are used.

Applications of PCR: Disease diagnosis, Research and cloning, Forensic analysis.Central Dogma of Molecular Biology




# Central Dogma 

The central dogma describes the flow of genetic information: DNA → RNA → Protein Replication: DNA makes identical copies of itself Transcription: DNA is transcribed into RNA Translation: RNA is translated into protein Post-translational modifications alter protein function These processes form the basis of genomics, transcriptomics, proteomics, and metabolomics, which together are studied in systems biology.

transcription: DNA is read, not consumed, during transcription. Produces mRNA, which carries genetic information to ribosomes. Discovery of mRNA (1961) confirmed RNA acts as a messenger between DNA and protein. Key points: Occurs 5’ → 3’, RNA polymerase synthesizes RNA, Transcription is the foundation of gene expression analysis (RNA-seq, qPCR)

tRNA as a Molecular Adaptor: tRNA (transfer RNA) delivers amino acids to ribosomes. Each tRNA binds a specific amino acid and matches it to mRNA codons. Confirms the adaptor hypothesis in protein synthesis. Role: Links nucleotide language (RNA) to amino acid language (protein).

Reverse Transcription: Reverse transcription converts RNA → DNA (cDNA). Discovered by Howard Temin and David Baltimore (1970). Catalyzed by reverse transcriptase. Applications: RT-PCR, RNA-seq, Studying gene expression from RNA samples. This expands the central dogma beyond one-way flow.


# FASTA file format:
it is used for sequencing.it contains only sequence information

# FASTQ file format:
it is used for sequencing and quality control sequence will start from @ then machine id then lane number than coordinates.it includes phred quality scoresFastQC – Quality Control of NGS Data. FastQC is a quality control tool used to analyze raw FASTQ files and identify potential sequencing issues before downstream analysis. -FastQC Output Modules: Per Base Sequence Quality. Displays quality scores across each base position in reads. Green region indicates high-quality bases. Yellow indicates moderate quality. Red indicates low-quality bases -GC Content: Shows the distribution of GC content across all reads. Helps identify contamination or biased sequencing -Adapter Contamination: Detects presence of adapter sequences in reads. Adapter contamination can affect alignment and must be removed if present -Sequence Duplication Levels: Indicates the level of duplicate reads. High duplication may suggest PCR bias or over-amplification



# Phred quality scores:
measures base accuracy


# BLAST Analysis and Primer Design for PCR
BLAST (Basic Local Alignment Search Tool) Why we use BLAST: Identify unknown sequences, Confirm gene identity, Check primer specificity, Compare sequences across organisms

Types of BLAST: -Megablast: For highly similar sequences (≥95% identity). -Discontiguous Megablast: For more divergent sequences. Cross-species comparisons. -BLASTn: General nucleotide sequence comparison. Used when similarity is moderate or unknown.

Understanding BLAST Output: Key parameters to check: -Query Coverage: % of query sequence aligned -Percent Identity: Exact base/residue matches -E-value: Near 0 → highly significant match, High value → match may be random -Alignment Length: Length of matching region -Max Score: Best single alignment score -Total Score: Sum of all alignment scores

BLAST in Primer Design: Used to check primer specificity. Ensures primers bind only to target gene. Helps avoid off-target amplification.

Basic Primer Design Rules: Length: 18–30 bases, GC content: 40–60%. Avoid: Secondary structures, Hairpins, Primer dimers Forward and reverse primers should have similar Tm (±5°C)

Melting Temperature (Tm) in PCR: Factors influencing Tm -Primer length: Longer → higher Tm -GC content: Higher GC → higher Tm -Salt concentration: Higher salt → higher Tm-Primer concentration Use of Tm in PCR: Annealing temperature (Ta) ≈ Tm – 5°C
