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




# Heatmap Analysis
After differential expression analysis using DESeq2, a heatmap was generated from the normalized expression matrix.

The heatmap visualizes gene expression patterns across samples.

Rows represent genes (often top differentially expressed genes).

Columns represent samples or conditions.

Color intensity indicates relative expression levels (e.g., high vs low expression).

Clustering helps identify: Similar expression profiles between samples. Groups of co-regulated genes


#  Molecular Epidemiology & Genomic Surveillance of SARS-CoV-2

Molecular Epidemiology: Combines molecular biology + epidemiology to track infectious diseases. Uses genome sequencing to study transmission, evolution, and spread of pathogens. Helps identify sources of infection, outbreak patterns, and variant emergence.


Genomic Surveillance in India (INSACOG): INSACOG: Indian SARS-CoV-2 Genomics Consortium. Objectives: Monitor emerging variants, Correlate variants with disease severity, Support public health decisions. Nationwide sequencing and data sharing.

Role of Genomics in COVID-19: Genome sequencing enabled identification of SARS-CoV-2 variants. Helped trace introduction, transmission, and persistence of variants in India. Supported monitoring of mutation patterns and geographic spread.


SARS-CoV-2 in India: First case detected in January 2020. Symptoms include fever, cough, breathlessness, loss of taste/smell. Genomic surveillance revealed multiple introductions and community transmission.

Variants of Interest (VOI) & Variants of Concern (VOC): Alpha (B.1.1.7), Delta (B.1.617.2), Gamma, etc. VOCs show: Increased transmissibility, Immune escape potential, Higher viral load. Classification based on genetic mutations and epidemiological impact.





# Virtual Design and Specificity Testing of GAPDH PCR Primers

Gene name:"Human GAPDH"

gene id: 2597

# Primer sequences

Primer pair 1

	Sequence (5'->3')

  Forward primer	CGTCGCCAGCCGAGC

  tm:60.64

  GC% : 80.00

  length : 15

  Reverse primer	GCCCAATACGACCAAATCCG

  tm:59.34

  GC% 55.00

  length: 20


  
  

Primer pair 2

	Sequence (5'->3')

  Forward primer	GCCAGCCGAGCCACAT

  tm: 59.71

  GC%  :68.75

  length : 16

  
Reverse primer	GCCCAATACGACCAAATCCGTTG

tm: 62.57

GC%  52.17

length : 23



Specificity of primersPrimer pairs are specific to input template as no other targets were found in selected database: Eukaryotic genomes (Refseq representative primary assembly + mitochondrion + plastid ) (Organism limited to Homo sapiens)


![Screenshot 2026-01-19 200051](https://github.com/user-attachments/assets/61f1f5e9-d92f-44e0-8e93-eb7cc18fc51a)




#  Identify an Unknown Biological
Sequence Using BLAST 

Sequence Observation

Given sequence number (Sequence 1):
1 CGGACACACAAAAAGAAAGAAGAATTTTTA GGATCTTTTGTGTGCGAATAACTATGAGGA
61 AGATTAATAATTTTCCTCTCATTGAAATTTATATCGGAATTTAAATTGAAATTGTTACTG
121 TAATCACACCTGGTTTGTTTCAGAGCCACATCACAAAGATAGAGAACAACCTAGGTCTCC
181 GAAGGGAGCAAGGGCATCAGTGTGCTCAGTTGAAAATCCC 


# Type of sequence:

DNA (contains A, T, G, C only)


# BLAST Tool Selection

BLAST program used:

BLASTn for DNA sequences

![Screenshot 2026-01-21 212256](https://github.com/user-attachments/assets/0c1c9540-89e9-4dfb-9fb1-14d619377049)



# BLAST Results 

(Top Hit Analysis)

Gene name:Zaire ebolavirus isolate Ebola virus/H.sapiens-rec/COD/1976/Yambuku-Mayinga-eGFP-BDBV_GP

Organism name : Zaire ebolavirus

Database used : core_nt

Percentage identity :100.00%

E-value:4e-109

![Screenshot 2026-01-21 212328](https://github.com/user-attachments/assets/de403282-067a-4e09-9071-a7e9f56295dd)


# Alignment Interpretation

Matching Regions

The alignment shows 220 out of 220 nucleotides matching between the query sequence and the subject sequence.

This corresponds to 100% identity, meaning every nucleotide in the query exactly matches the reference sequence.

The alignment is continuous from position 1 to 220, showing that the entire query sequence aligns with the reference genome.


# Gaps or Mismatches

No gaps are present in the alignment (Gaps: 0/220, 0%).

No mismatches are observed between the query and subject sequences.

Yes, the alignment strongly supports correct identification of the sequence.

![Screenshot 2026-01-21 212434](https://github.com/user-attachments/assets/0c0397f9-cfc5-4e86-a496-e68d7be5029f)


# Biological Function

 The Ebola virus genome encodes proteins involved in viral replication and infection of human cells. Since Ebola virus causes a severe infectious disease in humans, this sequence is considered to be disease-related in function.

 # Classification & Interpretation
 
Gene or Protein

The identified sequence is a gene and not a protein sequence, as it consists only of nucleotide bases (A, T, G, and C) and does not represent an amino acid sequence.


The sequence is species-specific, as it shows a 100% match to the Zaire ebolavirus genome and is not broadly conserved across unrelated organisms.


#  Final Conclusion 


The given unknown sequence is identified as gene from Zaire ebolavirus organism. BLAST analysis shows a % identity of 100.00% and an E-value of 4e-109, indicating a strong match.






# Sequence 2

1 CTCGAGGGGC CTAGACATTG CCCTCCAGAG AGAGCACCCA ACACCCTCCA GGCTTGACCG
61 GCCAGGGTGT CCCCTTCCTA CCTTGGAGAG AGCAGCCCCA GGGCATCCTG CAGGGGGTGC
121 TGGGACACCA GCTGGCCTTC AAGGTCTCTG CCTCCCTCCA GCCACCCCAC TACACGCTGC
181 TGGGATCCTG GATCTCAGCT CCCTGGCCGA CAACACTGGC AAACTCCTAC TCATCCACGA


# Type of sequence:

DNA (contains A, T, G, C only)


# BLAST Tool Selection

BLAST program used:

BLASTn for DNA sequences

![Screenshot 2026-01-21 225319](https://github.com/user-attachments/assets/844323e3-cf67-435d-98a4-14547cdcaf63)



# BLAST Results 

(Top Hit Analysis)


Gene name: Homo sapiens insulin (INS) gene

Organism name: Homo sapiens

Database used : core_nt

Percentage identity:100.00%

E-value:4e-120

![Screenshot 2026-01-21 225357](https://github.com/user-attachments/assets/8ad49581-c154-4936-989a-9d8912fe7bda)


# Alignment Interpretation

Matching Regions

Aligned range: 1–240 bp

Identities: 240/240 (100%)

This means every nucleotide in this 240 bp region matches perfectly with Homo sapiens insulin gene

 Gaps or mismatches

Gaps: 0/240 (0%)

Mismatches: None

The alignment lines show continuous |||||, confirming no substitutions, insertions, or deletions

![Screenshot 2026-01-21 225450](https://github.com/user-attachments/assets/8d9ed517-f00f-47af-8b59-efecc64cbe21)



#  Biological Function

The INS gene produces insulin, a hormone that controls blood sugar levels by helping cells absorb glucose.

Description:
Insulin helps regulate glucose metabolism and maintains energy balance in the body.

Functional category:
Metabolic; Disease-related (linked to diabetes) 


# Classification & Interpretation

Organism type: Eukaryotic

Conservation: Conserved across species


# Conclusion

The given unknown sequence is identified as  Homo sapiens insulin (INS) gene from Homo sapien organism. BLAST analysis shows a % identity of 100.00% and an E-value of 4e-120 indicating a strong match



# Sequence 3

MAGRSGDSDEDLLKAVRGIRGQYGTIYSLIEESQNQQEKNEQELLELDKW
ASLWNWFDITNWLWYIKIFIMIVGGLIGLRIVFAVLSIVNRVRQGYSPLS


# Type of sequence

Protein

# BLAST Tool Selection

BLAST program used:

BLASTp for protein sequences

![Screenshot 2026-01-21 234244](https://github.com/user-attachments/assets/3a9c1878-33f0-49b6-a3dd-8222ea8f3096)




# BLAST Results 

(Top Hit Analysis)


protein name:  Envelope glycoprotein gp160,Envelope glycoprotein gp160 

Organism name: Human immunodeficiency virus 1

Database used : core_nt

Percentage identity: 80.43%

E-value: 2e-44

![Screenshot 2026-01-21 234310](https://github.com/user-attachments/assets/ab637aef-c8d2-4ac2-93d6-91285ffc7888)


# Alignment Interpretation

Matching Regions













  
