# General Bioinformatic Workflow-to-reproduce-BP6-2022-paper
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
total reads: 72136133.
total bases: 11181100615.
Q20 bases: 10669942166(95.4284%).
Q30 bases: 10240561480(91.5881%).

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

fastp v0.20.1, time used: 1981 seconds

-----------------------------------------------------------------------------------------------------------------------
# Taxonomic Profile

    $ kaiju -t /mnt/f/kaiju/nodes.dmp  -f /mnt/f/kaiju/kaiju_db_progenomes.fmi   -i clean_varnish_shotgun_bp6_S3HiC_AD002_R1.fq  -j clean_varnish_shotgun_bp6_S3HiC_AD002_R2.fq -v -z 20 -o kaiju_out_bp6

15:58:08 Reading database

 Reading taxonomic tree from file /mnt/f/kaiju/nodes.dmp
 
 Reading index from file /mnt/f/kaiju/kaiju_db_progenomes.fmi
 
Output file: kaiju_out_bp6

15:59:00 Start classification using 20 threads.

16:46:37 Finished.

Creating input file for Krona

	kaiju2krona -t /mnt/f/kaiju/nodes.dmp  -n /mnt/f/kaiju/names.dmp  -i kaiju_out_bp6  -o kaiju.out_bp6.krona

The file kaiju.out.krona can then be imported into Krona and converted into an HTML file using Krona's ktImportText program:
ktImportText -o kaiju.out_bp6.html /mnt/f/Lecturas_Metagenomas/Hi_C_Reads_BP6_BP8/bp6_shotgun_reads_buenas/kaiju.out_bp6.krona

Creating classification summary

	kaiju2table -t /mnt/f/kaiju_db/nodes.dmp -n /mnt/f/kaiju_db/names.dmp -r genus -o kaiju_genusTotal_summary.tsv kaiju_out_bp6

--------------------------------------------------------------------------------------------------------------------------------

# GTDB-Tk v1.7.0 analysis

    $ gtdbtk identify --genome_dir gtdb_input/  --out_dir identify/ --extension fasta --cpus 4
    
    [2022-01-23 10:52:52] INFO: GTDB-Tk v1.7.0
[2022-01-23 10:52:52] INFO: gtdbtk identify --genome_dir gtdb_input/ --out_dir identify/ --extension fasta --cpus 4
[2022-01-23 10:52:52] INFO: Using GTDB-Tk reference data version r202: /home/ayixon/miniconda3/envs/gtdb/share/gtdbtk-1.7.0/db/
[2022-01-23 10:52:52] INFO: Identifying markers in 35 genomes with 4 threads.
[2022-01-23 10:52:52] TASK: Running Prodigal V2.6.3 to identify genes.
[2022-01-23 11:01:13] INFO: Completed 35 genomes in 8.35 minutes (4.19 genomes/minute).
[2022-01-23 11:01:13] TASK: Identifying TIGRFAM protein families.
[2022-01-23 11:04:22] INFO: Completed 35 genomes in 3.15 minutes (11.10 genomes/minute).
[2022-01-23 11:04:22] TASK: Identifying Pfam protein families.
[2022-01-23 11:04:56] INFO: Completed 35 genomes in 33.38 seconds (1.05 genomes/second).
[2022-01-23 11:04:56] INFO: Annotations done using HMMER 3.1b2 (February 2015).
[2022-01-23 11:04:56] TASK: Summarising identified marker genes.
[2022-01-23 11:05:01] INFO: Completed 35 genomes in 5.04 seconds (6.94 genomes/second).
[2022-01-23 11:05:01] INFO: Done.

    $ gtdbtk align --identify_dir identify/ --out_dir align --cpus 4
    
    [2022-01-23 11:23:18] INFO: GTDB-Tk v1.7.0
[2022-01-23 11:23:18] INFO: gtdbtk align --identify_dir identify/ --out_dir align --cpus 4
[2022-01-23 11:23:18] INFO: Using GTDB-Tk reference data version r202: /home/ayixon/miniconda3/envs/gtdb/share/gtdbtk-1.7.0/db/
[2022-01-23 11:23:19] INFO: Aligning markers in 35 genomes with 4 CPUs.
[2022-01-23 11:23:19] INFO: Processing 35 genomes identified as bacterial.
[2022-01-23 11:23:23] INFO: Read concatenated alignment for 45,555 GTDB genomes.
[2022-01-23 11:23:23] TASK: Generating concatenated alignment for each marker.
[2022-01-23 11:23:24] INFO: Completed 35 genomes in 1.35 seconds (25.92 genomes/second).
[2022-01-23 11:23:24] TASK: Aligning 120 identified markers using hmmalign 3.1b2 (February 2015).
[2022-01-23 11:23:35] INFO: Completed 120 markers in 10.28 seconds (11.67 markers/second).
[2022-01-23 11:23:35] TASK: Masking columns of bacterial multiple sequence alignment using canonical mask.
[2022-01-23 11:24:28] INFO: Completed 45,590 sequences in 53.56 seconds (851.27 sequences/second).
[2022-01-23 11:24:28] INFO: Masked bacterial alignment from 41,084 to 5,037 AAs.
[2022-01-23 11:24:28] INFO: 1 bacterial user genomes have amino acids in <10.0% of columns in filtered MSA.
[2022-01-23 11:24:29] INFO: Creating concatenated alignment for 45,589 bacterial GTDB and user genomes.
[2022-01-23 11:24:53] INFO: Creating concatenated alignment for 34 bacterial user genomes.
[2022-01-23 11:24:53] INFO: Done.

    $ gtdbtk classify --genome_dir gtdb_input/ -x fasta --align_dir align/  --out_dir classify_output --cpus 4

[2022-01-23 11:37:39] INFO: GTDB-Tk v1.7.0
[2022-01-23 11:37:39] INFO: gtdbtk classify --genome_dir gtdb_input/ -x fasta --align_dir align/ --out_dir classify_output --cpus 4
[2022-01-23 11:37:39] INFO: Using GTDB-Tk reference data version r202: /home/ayixon/miniconda3/envs/gtdb/share/gtdbtk-1.7.0/db/
[2022-01-23 11:37:40] WARNING: pplacer requires ~215 GB of RAM to fully load the bacterial tree into memory. However, 18.31 GB was detected. This may affect pplacer performance, or fail if there is insufficient swap space.
[2022-01-23 11:37:40] TASK: Placing 34 bacterial genomes into reference tree with pplacer using 4 CPUs (be patient).
[2022-01-23 11:37:40] INFO: pplacer version: v1.1.alpha19-0-g807f6f3
==> Running pplacer v1.1.alpha19-0-g807f6f3 analysis on align/align/gtdbtk.bac120.user_ms==> 
Step 2 of 9: Pre-masking sequences.

==> Step 6 of 9: Pulling exponents.                                                          Process Process-1:
.....
classify_output/classify/intermediate_results/pplacer/pplacer.bac120.out

================================================================================
________________________________________________________________________________

# Anvio_Taxonomy

Database for contigs_bins

#!/bin/bash 
for i in  bin_16.fasta  bin_23.fasta  bin_30.fasta  bin_6.fasta bin_1.fasta             bin_17.fasta  bin_24.fasta  bin_31.fasta  bin_7.fasta bin_10.fasta            bin_18.fasta  bin_25.fasta  bin_32.fasta  bin_8.fasta bin_11.fasta            bin_19.fasta  bin_26.fasta  bin_33.fasta  bin_9.fasta bin_12.fasta            bin_2.fasta   bin_27.fasta  bin_34.fasta bin_13.fasta            bin_20.fasta  bin_28.fasta  bin_35.fasta bin_14.fasta            bin_21.fasta  bin_29.fasta  bin_4.fasta bin_15.fasta            bin_22.fasta  bin_3.fasta   bin_5.fasta

do anvi-gen-contigs-database -f "$i" -o "$i".db -T 20

done

echo "Contig database"

================================================================================
# Anvio workFlow per bin:


	$ anvi-setup-scg-taxonomy --reset

	$ anvi-run-hmms -c contig.db --num-threads 20 --just-do-it

	$ anvi-run-scg-taxonomy -c contig.db
    
    $ anvi-estimate-scg-taxonomy -c contig.db
    
 ================================================================================
 
 # UBCG: Phylogenomic tree reconstruction with  Up-to-date bacterial core gene set pipeline (UBCG)
 
 BCG prediction
 
	 #!/bin/bash 

	for i in  bin_1.fasta... bin_n.fasta   

	do java -jar UBCG.jar extract -bcg_dir bcg -i fasta/$i -label $i -t 23 

	done 

	echo "BCG prediction Done"

Running UBCGpipeline

	$ java -jar UBCG.jar align -bcg_dir bcg -prefix 2022_Phylogenomic_bp6
	
          ##############################
          #         UBCG_align         #
          ##############################
	Reading bcg files..
 	All of the gene trees were reconstructed.

	Calculating Gene Support Indices (GSIs) from the gene trees..

	The final tree marked with GSI was written to 'output/2022_Phylogenomica_bp6/2022_Phylogenomica_bp6.UBCG_gsi(92).codon.50.label.nwk'
------------------------------------------------------------------------------------------------------------------------------------------------
# enrichm  Annotation
	enrichm annotate --protein_directory input_enrichM_metagenome/ --threads 3 --ko --pfam  --output input_enrichM_metagenome/enrichM_annotate
	/usr/local/lib/python3.8/dist-packages/fuzzywuzzy/fuzz.py:11: UserWarning: Using slow pure-python SequenceMatcher. Install python-Levenshtein to remove this warning
 	 warnings.warn('Using slow pure-python SequenceMatcher. Install python-Levenshtein to remove this warning')
	[2022-02-01 13:03:23 PM] INFO: Command: /usr/local/bin/enrichm annotate --protein_directory input_enrichM_metagenome/ --threads 3 --ko --pfam --output 			input_enrichM_metagenome/enrichM_annotate
	[2022-02-01 13:03:23 PM] INFO: Running the annotate pipeline
	[2022-02-01 13:03:24 PM] INFO: Running pipeline: annotate
	[2022-02-01 13:03:24 PM] INFO: Setting up for genome annotation
	[2022-02-01 13:03:24 PM] INFO: Using provided proteins
	[2022-02-01 13:03:24 PM] INFO: Preparing genomes for annotation
	[2022-02-01 13:03:28 PM] INFO: Starting annotation:
	[2022-02-01 13:03:28 PM] INFO:     - Annotating genome(s) with ko ids using DIAMOND
	[2022-02-01 13:03:28 PM] INFO:     - BLASTing genome(s)
	[2022-02-01 13:50:04 PM] INFO:     - Generating ko frequency table
	[2022-02-01 13:50:04 PM] INFO:     - Writing results to file: input_enrichM_metagenome/enrichM_annotate/ko_frequency_table.tsv
	
	------------------------------------------------------------------------------------------------------------------------------------------------
# MGWAS with pyseer

		1-Prediction of  kmers with unitig caller:
--------------------------------------------------
		$ unitig-counter -strains  input.txt -output output -nb-cores 20

Stats:
Number of kmers: 823092427
Number of unitigs: 7850499
################################################################################
[Starting mapping process... ]
Using 20 cores to map 18 read files.
966800 reads processed.
[Mapping process finished!]
[Transpose pattern matrix..]
[Generating pyseer input]...
Number of unique patterns: 25613
[Generating pyseer input] - Done!
Done!
################################################################################

#############################################################################################################

		2-Running pysser on:
--------------------------------------------------

pyseer --lmm --phenotypes polyurethanolytic.phenotype.txt --kmers BP6_unitigs.txt.gz  --similarity phylogeny_K.tsv  --output-patterns kmer_patterns.txt \
--cpu 24 > poliurethane_kmers.txt
Read 18 phenotypes
Detected binary phenotype
Setting up LMM
Similarity matrix has dimension (18, 18)
Analysing 18 samples found in both phenotype and similarity matrix
h^2 = 1.00
7850499 loaded variants
13800 pre-filtered variants
7836699 tested variants
7836699 printed variants

###########################################################################################################################

	 3-Estimate "significance threshold"  using the number of unique k-mer patterns
--------------------------------------------------

		$ python count_pattern.py kmer_patterns.txt
	Patterns:       24297
	Threshold:      2.06E-06

#############################################################################################################################
		
	4-Interpreting significant k-mers
--------------------------------------------------

cat <(head -1 poliurethane_kmers.txt) <(awk '$4<2.06E-06 {print $0}' poliurethane_kmers.txt) > significant_kmers.txt

	
	145127 significant kmers
...many of them are false positives due to their short length...

	...manually curing short sequences (< 50pb)

#############################################################################################################################
#############################################################################################################################

	Read 145127 k-mers

Causal efective after curing 27450 k-mers

#############################################################################################################################
#############################################################################################################################


