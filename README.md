# Variant-calling-analysis
NGS pipeline for variant calling
Homo-Sapians dataset was used for varaint calling analysis starting from the quality check to annotation.
# Quality Check
FastQC is used to assess the quality of raw sequencing data. It generates reports on read quality, GC content, adapter contamination, sequence duplication levels, and other metrics.
Checking data quality is very important before proceding to the trimming and alignment.
# Trimming
Fastp tool was utilized to filter out low quality bases, adapters and other unwanted sequences from raw reads.This step ensures the high quality reads are used.
# Alignment
BWA tool was used to map the reads using reference genome (hg38). This step produces the aligment files in SAM format.
# Sorting
SAM file was converted into the BAM file with the help of SAMtools which is further sorted by genomic coordinates to prepare them for variant calling.
# Variant Calling
variant calling focuses on identifying the genomic differences (i.e SNPs and indels) between reference genome and aligned reads.freebayes identifies the variants by generating the variant call format files (VCF).
# Annotation
Annotation was performed using the SnpEff tool which helps to predict the variants effects on genes and proteins. bcfttols were occupied to manipulate and filter VCF files. Therefore, potentially significant variants are identified to explore further biological interpretation. 
