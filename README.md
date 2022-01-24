# Workflow-to-reproduce-BP6-2022-paper
Scripts used for the metagenomic analysis of the paper: 
# "Biodegradation of a polyether-polyurethane-acrylic copolymer by a landfill microbial community. Genetic basis   inferred from metagenomic deconvolution analysis "

# Metagenome Deconvolution from Phasegenomics:
------------------------------------------------------
Assembly length (bp):	154,504,017 ||| Number of contigs total:15,727 ||| Number of contigs in clusters:8,072 ||| 

Percent assembly length in clusters:86.62 ||| Percent contigs in clusters:51.33

------------------------------------------------------

Total clusters:35

Complete clusters (>95% complete, <10% MGO):19 ||| Excellent clusters (>90% complete, <10% MGO):23

Good clusters (>70% complete, <10% MGO):29 ||| Reasonable clusters (>50% complete, <10% MGO):31

------------------------------------------------------
SAMPLE DETAILS   Name: bp6_newbins_rerun

Creator: ayixon.sanchez@mail.ibt.unam.mx; Created: Nov. 19, 2021; Updated: Nov. 19, 2021

Contig fasta file(s): bp6_newbins_contigs.fasta

Alignment file(s): bp6_newbins_s3_m1.bam; bp6_newbins_rerun_s3_m1.bam

-------------------------------------------------------
# Preprocessing of shotgun FastQ files
    $ fastp -i varnish_shotgun_bp6_S3HiC_AD002_R1.fastq  -I varnish_shotgun_bp6_S3HiC_AD002_R2.fastq  -w 20 -o clean_varnish_shotgun_bp6_S3HiC_AD002_R1.fq -O   clean_varnish_shotgun_bp6_S3HiC_AD002_R2.fq


Read1 before filtering:
total reads: 72136133
total bases: 11181100615
Q20 bases: 10669942166(95.4284%)
Q30 bases: 10240561480(91.5881%)

Read2 before filtering:
total reads: 72136133
total bases: 11181100615
Q20 bases: 10377167018(92.8099%)
Q30 bases: 9827561570(87.8944%)

Read1 after filtering:
total reads: 69635576
total bases: 10383950380
Q20 bases: 10011089372(96.4093%)
Q30 bases: 9632495490(92.7633%)

Read2 aftering filtering:
total reads: 69635576
total bases: 10385001031
Q20 bases: 9775940004(94.1352%)
Q30 bases: 9294460764(89.4989%)

Filtering result:
reads passed filter: 139271152
reads failed due to low quality: 4837100
reads failed due to too many N: 8662
reads failed due to too short: 155352
reads with adapter trimmed: 11158812
bases trimmed due to adapters: 473523680

Duplication rate: 4.80288%

Insert size peak (evaluated by paired-end reads): 279

JSON report: fastp.json
HTML report: fastp.html

fastp -i varnish_shotgun_bp6_S3HiC_AD002_R1.fastq -I varnish_shotgun_bp6_S3HiC_AD002_R2.fastq -w 20 -o clean_varnish_shotgun_bp6_S3HiC_AD002_R1.fq -O clean_varnish_shotgun_bp6_S3HiC_AD002_R2.fq
fastp v0.20.1, time used: 1981 seconds
