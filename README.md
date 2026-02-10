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
**sudo apt install bwa**
**conda install -c bioconda bwa**
**bwa index hg38.fna**
**bwa mem hg38.fna output_FW.fastq output_REV.fastq > output.sam**

# Sorting
SAM file was converted into the BAM file with the help of SAMtools which is further sorted by genomic coordinates to prepare them for variant calling.
**sudo apt install samtools**
**samtools view output.sam**
**samtools index output.sam**
**samtools view -bS output.sam > output.bam**
**samtools sort -o sorted.bam output.bam**
**samtools index sorted.bam**
**samtools view sorted.bam**

# Variant Calling
variant calling focuses on identifying the genomic differences (i.e SNPs and indels) between reference genome and aligned reads.freebayes identifies the variants by generating the variant call format files (VCF).
**sudo apt install freebayes**
**freebayes -f hg38.fna sorted.bam > output.vcf**
**wget https://github.com/freebayes/freebayes/releases/download/v1.3.9/freebayes-v1.3.9-linux-amd64.gz**
**gunzip freebayes-v1.3.9-linux-amd64.gz**
**chmod +x freebayes-v1.3.9-linux-amd64**
**conda create -n freebayes_env**
**conda activate freebayes_env**
**Install FreeBayes from bioconda (with conda-forge as dependency channel)**
**conda install -c conda-forge -c bioconda freebayes**
**conda activate freebayes_env**
**freebayes -f hg38.fna sorted.bam > output.vcf**
# Annotation
Annotation was performed using the SnpEff tool which helps to predict the variants effects on genes and proteins. bcftools were occupied to manipulate and filter VCF files. Therefore, potentially significant variants are identified to explore further biological interpretation. 

**sudo apt install snpeff**
**wget https://snpeff.blob.core.windows.net/versions/snpEff_latest_core.zip**
**unzip snpEff_latest_core.zip**
**conda create -n SNPEFF_ENV**
**conda config --add channels defaults**
**conda config --add channels bioconda**
**conda config --add channels conda-forge**
**activate snp environment**
**java -jar snpEff.jar databases (to see all available genome version)**
**java -jar snpEff.jar GRCh38.99 output.vcf > annotated.vcf** 
**snpEff ann GRCh38.86 output.vcf > annotated.vcf**



