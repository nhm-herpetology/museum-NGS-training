# Bioinformatics Laboratory 3
>You will need a Unix Command Terminal or PuTTY interface to complete this lab. 

**Overvew**

To identify UCEs from targeted sequence capture data there are five main steps:

1. Clean raw FASTQ files for quality and adpater contamination.
2. Organise cleaned data by individuals/species
3. *de novo* assemble contigs 
4. Identify contigs that include UCEs from each individual/species
5. Sort UCEs into appropriate directories
>For phylogenetic analyses etc., UCEs can then be aligned across all species/individuals. 

## Processing UCE data with phyluce

<details>
  <summary>Click to expand content!</summary>

>As we already learned in [Unit 1](https://github.com/nhm-herpetology/museum-NGS-training/tree/main/Unit_01/Bioinformatics_Lab) and [Unit 2](https://github.com/nhm-herpetology/museum-NGS-training/tree/main/Unit_02/Bioinformatics_Lab), phyluce is a really helpful program for processing targeted sequence capture data. There are several tutorials avialable here [here](https://phyluce.readthedocs.io/en/latest/tutorials/index.html)


1. Navigate to the SRA tools ```bin``` directory from [Unit 1](https://github.com/nhm-herpetology/museum-NGS-training/tree/main/Unit_01/Bioinformatics_Lab). We will download some raw data from three more snake species from the Streicher & Wiens [2016](https://www.sciencedirect.com/science/article/abs/pii/S1055790316300495?via%3Dihub) dataset; *Xenodermus javanicus*, *Micrurus fulvius*, and *Loxocemus bicolor*.

```
./fasterq-dump SRR3284492	
```
>The *X. javanicus* download should take ~4-5 minutes with an output of:  
```
spots read      : 727,334
reads read      : 1,454,668
reads written   : 1,454,668	
```   

```
./fasterq-dump SRR3284197	
```
 >The *M. fulvius* download should take ~3-4 minutes with an output of: 
```
spots read      : 560,385
reads read      : 1,120,770
reads written   : 1,120,770
```
  
```
./fasterq-dump SRR3284196		
```
>The *L. bicolor* download should take ~2-3 minutes with an output of:
```
spots read      : 256,289
reads read      : 512,578
reads written   : 512,578		
```  
  
2. Now, we will move these new files to our phyluce directory from [Unit 1](https://github.com/nhm-herpetology/museum-NGS-training/tree/main/Unit_01/Bioinformatics_Lab):

```
mv SRR3284492_1.fastq /home/jefs/NGS_course/Unit_1/Data/raw-fastq
```  
```
mv SRR3284492_2.fastq /home/jefs/NGS_course/Unit_1/Data/raw-fastq
```   
```
mv SRR3284197_1.fastq /home/jefs/NGS_course/Unit_1/Data/raw-fastq
```  
```
mv SRR3284197_2.fastq /home/jefs/NGS_course/Unit_1/Data/raw-fastq
```    
```
mv SRR3284196_1.fastq /home/jefs/NGS_course/Unit_1/Data/raw-fastq
```  
```
mv SRR3284196_2.fastq /home/jefs/NGS_course/Unit_1/Data/raw-fastq
```     

3. Now navigate to the 'Data/raw-fastq' directory. Let's prepare the files for cleaning by renaming them and compressing them: 
```
mv SRR3284492_1.fastq SRR3284492_S1_L001_R1_001.fastq
```
```
mv SRR3284492_2.fastq SRR3284492_S1_L001_R2_001.fastq
``` 
```
gzip SRR3284492_S1_L001_R1_001.fastq
```  
```
gzip SRR3284492_S1_L001_R2_001.fastq
```
>These compression steps might take a few minutes...
```
mv SRR3284197_1.fastq SRR3284197_S1_L001_R1_001.fastq
```  
```
mv SRR3284197_2.fastq SRR3284197_S1_L001_R2_001.fastq
``` 
```
gzip SRR3284197_S1_L001_R1_001.fastq
```  
```
gzip SRR3284197_S1_L001_R2_001.fastq
```
>These compression steps might take a few minutes...  
```
mv SRR3284196_1.fastq SRR3284196_S1_L001_R1_001.fastq
```  
```
mv SRR3284196_2.fastq SRR3284196_S1_L001_R2_001.fastq
``` 
```
gzip SRR3284196_S1_L001_R1_001.fastq
```  
```
gzip SRR3284196_S1_L001_R2_001.fastq
``` 
>Now navigate back up to the ```Data``` directory. 
  
4. Before we run illumiprocessor, let's remove the ```clean-fastq``` directory and the ```illumiprocessor.conf``` + ```illumiprocessor.log``` files from [Unit 1](https://github.com/nhm-herpetology/museum-NGS-training/tree/main/Unit_01/Bioinformatics_Lab):
  
```
rm -r clean-fastq
```
```
rm illumiprocessor.conf
``` 
```
rm illumiprocessor.log
```    
  
5. Now we will run Illumiprocessor, but an updated configuration file is needed. The configuration file should look like this:

```
[adapters]
i7:AGATCGGAAGAGCACACGTCTGAACTCCAGTCAC*ATCTCGTATGCCGTCTTCTGCTTG
i5:AGATCGGAAGAGCGTCGTGTAGGGAAAGAGTGTAGATCTCGGTGGTCGCCGTATCATT

[tag sequences]  
INDEX-16:CCGTCCCG
INDEX-17:GTCCGCAC
INDEX-32:CAGCGTTA
INDEX-41:CTCAATGA
  
[tag map]
SRR3284185_S1:INDEX-16
SRR3284197_S1:INDEX-17    
SRR3284492_S1:INDEX-32
SRR3284196_S1:INDEX-41  
  
[names]
SRR3284185_S1:Cylindrophis_ruffus_FMNH_258674
SRR3284197_S1:Micrurus_fulvius_YPM_14096  
SRR3284492_S1:Xenodermus_javanicus_FMNH_230073
SRR3284196_S1:Loxocemus_bicolor_ZA_46400  
  
```  

6. To make the configuration text file let's use the command line: 
 
 ```  
  cat > illumiprocessor.conf
 ```   
 Now paste the configuration text (from Step 5) into your terminal and then press CTRL + SHIFT + D.   
 
7. We are now ready to run Illumiprocessor to trim low quality bases + remove adapter contamiantion: 
 ```   
illumiprocessor \
    --input raw-fastq/ \
    --output clean-fastq \
    --config illumiprocessor.conf \
    --cores 4  
 ```   
>This should take ~3 minutes to run 
  
8. We need to update the assembly configuration file from [Unit 2](https://github.com/nhm-herpetology/museum-NGS-training/tree/main/Unit_02/Bioinformatics_Lab) to assemble reads into contigs. The configuration file should look like this:

```
[samples]
Cylindrophis_ruffus_FMNH_258674:clean-fastq/Cylindrophis_ruffus_FMNH_258674/split-adapter-quality-trimmed/
Micrurus_fulvius_YPM_14096:clean-fastq/Micrurus_fulvius_YPM_14096/split-adapter-quality-trimmed/  
Xenodermus_javanicus_FMNH_230073:clean-fastq/Xenodermus_javanicus_FMNH_230073/split-adapter-quality-trimmed/ 
Loxocemus_bicolor_ZA_46400:clean-fastq/Loxocemus_bicolor_ZA_46400/split-adapter-quality-trimmed/  
  
```  

9. To remove the old file and make the updated configuration text file let's use the command line: 
 
```  
rm assembly.conf
``` 
```  
cat > assembly.conf
```   
 Now paste the configuration text (from Step 8) into your terminal and then press CTRL + SHIFT + D.   

10. We are now ready to assemble the reads into contigs using velvet, but first we will remove the velvet-assemblies directory and log file from [Unit 2](https://github.com/nhm-herpetology/museum-NGS-training/tree/main/Unit_02/Bioinformatics_Lab): 

```  
rm -r velvet-assemblies
``` 
```  
rm phyluce_assembly_assemblo_velvet.log
```   
```   
phyluce_assembly_assemblo_velvet \
    --conf assembly.conf \
    --output velvet-assemblies \
    --cores 12 
 ```  
>This should take ~12-13 minutes to run. Now we are ready to identify which contigs correspond to UCE loci. 
  
11. Download the Tetrapod 5k probe sequences (this will be used to identify UCEs from the capture data). The probe set can also be downloaded [here](https://www.ultraconserved.org/)
  
```
wget https://raw.githubusercontent.com/nhm-herpetology/museum-NGS-training/main/Unit_03/Bioinformatics_Lab/Tetrapods-UCE-5Kv1.fasta
``` 

12. Now we will identify which contigs are UCEs: 

```  
phyluce_assembly_match_contigs_to_probes \
    --contigs velvet-assemblies/contigs \
    --probes Tetrapods-UCE-5Kv1.fasta \
    --output uce-search-results  
```
We should see something similar to the following output: 
  
```
2021-09-21 19:21:24,334 - phyluce_assembly_match_contigs_to_probes - INFO - Cylindrophis_ruffus_FMNH_258674: 2365 (4.81%) uniques of 49160 contigs, 0 dupe probe matches, 203 UCE loci removed for matching multiple contigs, 2 contigs removed for matching multiple UCE loci
2021-09-21 19:21:39,173 - phyluce_assembly_match_contigs_to_probes - INFO - Loxocemus_bicolor_ZA_46400: 1924 (2.50%) uniques of 76848 contigs, 0 dupe probe matches, 200 UCE loci removed for matching multiple contigs, 2 contigs removed for matching multiple UCE loci
2021-09-21 19:22:16,960 - phyluce_assembly_match_contigs_to_probes - INFO - Micrurus_fulvius_YPM_14096: 1315 (0.64%) uniques of 204962 contigs, 0 dupe probe matches, 228 UCE loci removed for matching multiple contigs, 2 contigs removed for matching multiple UCE loci
2021-09-21 19:22:57,398 - phyluce_assembly_match_contigs_to_probes - INFO - Xenodermus_javanicus_FMNH_230073: 1308 (0.56%) uniques of 234241 contigs, 0 dupe probe matches, 288 UCE loci removed for matching multiple contigs, 1 contigs removed for matching multiple UCE loci

```
  
13. Now we need to make a configuration file for extracting UCE data from this probe sequence matching step: 

```  
[all]
Cylindrophis_ruffus_FMNH_258674
Micrurus_fulvius_YPM_14096
Xenodermus_javanicus_FMNH_230073
Loxocemus_bicolor_ZA_46400
```
  
14. To make the configuration file: 
  
```  
cat > taxon-set.conf
```   
Now paste the configuration text (from Step 13) into your terminal and then press CTRL + SHIFT + D.   

15. It is time to extract UCEs from the taxa in our configuration file + make a directory to hold the information:  
``` 
mkdir -p taxon-sets/all
```  
```   
phyluce_assembly_get_match_counts \
    --locus-db uce-search-results/probe.matches.sqlite \
    --taxon-list-config taxon-set.conf \
    --taxon-group 'all' \
    --incomplete-matrix \
    --output taxon-sets/all/all-taxa-incomplete.conf  
``` 
 
16. Now we need to extract the UCE sequence data in the form of taxon-specific FASTA files: 

```  
cd taxon-sets/all  
```
```  
mkdir log
```  
```
cd ..
```
```
cd ..
```  
```  
phyluce_assembly_get_fastas_from_match_counts \
    --contigs velvet-assemblies/contigs \
    --locus-db uce-search-results/probe.matches.sqlite \
    --match-count-output taxon-sets/all/all-taxa-incomplete.conf \
    --output taxon-sets/all/all-taxa-incomplete.fasta \
    --incomplete-matrix taxon-sets/all/all-taxa-incomplete.incomplete \
    --log-path taxon-sets/all/log  
```   
  
The output should look something like this: 

```  
2021-09-21 19:33:53,819 - phyluce_assembly_get_fastas_from_match_counts - INFO - -------Getting UCE loci for Cylindrophis_ruffus_FMNH_258674------
2021-09-21 19:33:54,608 - phyluce_assembly_get_fastas_from_match_counts - INFO - There are 2365 UCE loci for Cylindrophis_ruffus_FMNH_258674
2021-09-21 19:33:54,608 - phyluce_assembly_get_fastas_from_match_counts - INFO - Parsing and renaming contigs for Cylindrophis_ruffus_FMNH_258674
2021-09-21 19:34:11,303 - phyluce_assembly_get_fastas_from_match_counts - INFO - Writing missing locus information to /home/jefs/NGS_course/Unit_1/Data/taxon-sets/all/all-taxa-incomplete.incomplete
2021-09-21 19:34:11,305 - phyluce_assembly_get_fastas_from_match_counts - INFO - ---------Getting UCE loci for Loxocemus_bicolor_ZA_46400---------
2021-09-21 19:34:11,909 - phyluce_assembly_get_fastas_from_match_counts - INFO - There are 1924 UCE loci for Loxocemus_bicolor_ZA_46400
2021-09-21 19:34:11,910 - phyluce_assembly_get_fastas_from_match_counts - INFO - Parsing and renaming contigs for Loxocemus_bicolor_ZA_46400
2021-09-21 19:34:38,183 - phyluce_assembly_get_fastas_from_match_counts - INFO - Writing missing locus information to /home/jefs/NGS_course/Unit_1/Data/taxon-sets/all/all-taxa-incomplete.incomplete
2021-09-21 19:34:38,184 - phyluce_assembly_get_fastas_from_match_counts - INFO - ---------Getting UCE loci for Micrurus_fulvius_YPM_14096---------
2021-09-21 19:34:38,616 - phyluce_assembly_get_fastas_from_match_counts - INFO - There are 1315 UCE loci for Micrurus_fulvius_YPM_14096
2021-09-21 19:34:38,616 - phyluce_assembly_get_fastas_from_match_counts - INFO - Parsing and renaming contigs for Micrurus_fulvius_YPM_14096
2021-09-21 19:35:44,490 - phyluce_assembly_get_fastas_from_match_counts - INFO - Writing missing locus information to /home/jefs/NGS_course/Unit_1/Data/taxon-sets/all/all-taxa-incomplete.incomplete
2021-09-21 19:35:44,492 - phyluce_assembly_get_fastas_from_match_counts - INFO - ------Getting UCE loci for Xenodermus_javanicus_FMNH_230073------
2021-09-21 19:35:44,882 - phyluce_assembly_get_fastas_from_match_counts - INFO - There are 1308 UCE loci for Xenodermus_javanicus_FMNH_230073
2021-09-21 19:35:44,882 - phyluce_assembly_get_fastas_from_match_counts - INFO - Parsing and renaming contigs for Xenodermus_javanicus_FMNH_230073
```  
>This has now extracted contigs that correspond to UCEs for each taxon into a single file called ```all-taxa-incomplete.fasta``` with contents that look like this: 
```  
>uce-5022_Cylindrophis_ruffus_FMNH_258674 |uce-5022
TTTGATGGGAATTGAATTTGATACCGCATTATGGTCGTAGGGCCTCCCCACAATAGACTG
TGTTCTTTGCTGTGTCTGTGCACAATCAGAGAGACCCAATTAAATAATTTGGTGCAATAA
TGGAGAACAAAAGCAGACGAGGGCTTAAAGTGAGGGCTGGAGCATTTGTAGTCTCCTC
>uce-129_Cylindrophis_ruffus_FMNH_258674 |uce-129
AGGGAAATCTGAGGCTTCCACTGCAGCACCATGCTTAGTAAGTAATAAATTACATGTTAT
ACTTATTTGCCTTAATTCATGCTAATTTTGTCCAATTAATGTATCACAGTAATTCAGAAG
CCTGTCACAGGAGAGCTAATTATTTATTGGATTTTTGTGTTTGGCTCCCTAGGAGTCTGC
TAGCAAACAAACTTATGAACATCTTTCCATTTGGGCCATGGTGACATTCTTATGTCTTAT
TAGGAAGAAAAGTTCTGTTCTTCAAAAAGTGAGCCATTATTCACTCAAGATACCATCTCT
TTGTTGTTCAATTGTAACAGCAAGAACATTCTCCTGTTTTACAAAGGATATGATGCAATG
TATTCCTTTCCCATCTAATTCTTTCCTTTATGCATCTAAATC
```

This FASTA file can now be used to align UCEs from different taxa and prepare them for comparative analyses.   
  
</details>

## Preparing UCE data for comparative analyses

<details>
  <summary>Click to expand content!</summary>

>After the last module, we have UCE data for all taxa in a single FASTA file. We will now learn how to align these sequence data for comparative analyses. 

1. We need to navigate to the taxon-sets directory we want to align.   
  
```
cd uce-tutorial/taxon-sets/all
```

2. Now we will align the UCEs using the software [MAFFT](https://mafft.cbrc.jp/alignment/software/) via the following command: 

```  
phyluce_align_seqcap_align \
    --input all-taxa-incomplete.fasta \
    --output mafft-nexus-edge-trimmed \
    --taxa 4 \
    --aligner mafft \
    --cores 12 \
    --incomplete-matrix \
    --log-path log  
```
>There will be several warning about 'dropped' UCEs - this is normal as the script works its way through all possible UCEs. 
 
3. Now let's have a look at the alignments: 

```
cd mafft-nexus-edge-trimmed
```
```   
ls  
```   
>You should see hundreds of files that correspond to alignments for all UCEs that the four snakes had in common. 
 
4. Looking at one of the NEXUS-formatted file: 
```   
cat uce-1013.nexus  
```  
We should see the following: 
```
#NEXUS
begin data;
dimensions ntax=3 nchar=195;
format datatype=dna missing=? gap=-;
matrix
'uce-1013_Cylindrophis_ruffus_FMNH_258674' ???????????????????????????????????????????????????????????????????????????????GGGTAGTTAAAATTCAGAAAGAGAAATTCCTTAATTAACTTAATAAAATTACTAATGGAAGCATTTTAACTGCTAAATTTAATTTACTTGTCAAGATATCCAGCTACAAAGAGTAG
'uce-1013_Loxocemus_bicolor_ZA_46400'      TTGTTCTCATACTCTTGTGGTTACTAAATATGTTGCGTTATATTATTTAAAAAAATAAATGAAGGTTCTTCTGAAATGAGGGTAGTTAAAATTCAGAAAGAGAAATTTCTTAATTAACTTAATAAAATTACTAATGGAAGCATTTTAACTGCTAAATTTAATTTACTTGTCAAGATATCCGGCTACAAAGA????
'uce-1013_Micrurus_fulvius_YPM_14096'      TTGTTATTAAACTCTTGTGGTTATCAAATATGTAGCAGTAT----------TAAAAAAATTAAAGTTGTGCTGAAATAAGGGTAGTTAAAATTCAGAAAGAGAAATTCCTTAATTAACTTAATAAAATTACTAATGGAAGCATTTTAGCGGCTAAATTTAATTTTCTTGTCAAGATATCCAGCTACAAAGAGTAG
;
end;  
```
>You can see that we have both '?' characters for missing edges and '-' characters for indels in the alignments. We also see that for UCE 1013, we lack data for *Xenodermus javanicus*.
  
</details>

## Mapping UCE data to genomic assemblies

<details>
  <summary>Click to expand content!</summary>

>We can align UCEs (or any locus) to genomic assemblies to see where each UCE is in the genome, which may help with understanding dynamics related to linkage etc. 

We will use the vertebrate 5k UCE probe sequences in FASTA format that we downloaded in the first module and chromosomes 6 (80.74 Mbp) of *Anolis carolinensis* as an example of mapping UCEs to a reference genome.   

1. We should have the NCBI Entrez Direct UNIX E-utilities installed from the [Unit 2](https://github.com/nhm-herpetology/museum-NGS-training/tree/main/Unit_02/Bioinformatics_Lab) bioinformatics lab. so that we can download genomic sequences 
  
```
cd edirect
```
  
2. To download Chromosome 6 from *Anolis carolinensis* we use:

```  
./esearch -db nucleotide -query "NC_014781.1" | ./efetch -format fasta > NC_014781.1.fasta
```
>It is a large file (~79 MB), so it should take ~2 minutes to download.
 
3. Now let's move it to the same folder as the FASTA file: 

```  
mv NC_014781.1.fasta /home/jefs/NGS_course/Unit_3
```
>Please navigate to the Unit_3 directory
  
4. If you haven't done so already, activate phyluce so that ```bwa``` and ```samtools``` are available:
  
```
conda activate phyluce-1.7.1
```
  
5. Let's Index chromosome 6 of *Anolis carolinensis* as a reference sequence:
  
```
bwa index NC_014781.1.fasta
```  
>This should take ~2 minutes  

6. Let's align the UCE probe/bait sequences to the reference: 

```  
bwa mem NC_014781.1.fasta Tetrapods-UCE-5Kv1.fasta -t 4 > bwa_mem_align_UCEs_c6.sam  
```  
  
7. Convert the sam file to a bam file  
 
``` 
samtools view -S -b bwa_mem_align_UCEs_c6.sam > UCE_Ac_6.bam 
```  
  
8. Now we sort the bam file: 
 
```  
samtools sort UCE_Ac_6.bam  -o UCE_Ac_6.sorted.bam 
```  
  
9. Finally, we index the sorted bam file and (if you want) view: 
 
```  
samtools index UCE_Ac_6.sorted.bam 
```   
```  
samtools tview UCE_Ac_6.sorted.bam AB179619.1.fasta NC_014781.1.fasta
```   

10. Let's get a list of the mapped sequences and then count how many mapped:

```   
samtools view -F 4 UCE_Ac_6.bam > mapped_C6.sam
```   
``` 
wc -l mapped_C6.sam  
```  
>There should be 273 probes that mapped to the *Anolis carolinensis* chromosome 6
  
</details>


**Helpful Links**
>[UCEs](https://www.ultraconserved.org/) | [phyluce](https://phyluce.readthedocs.io/en/latest/) | [MAFFT](https://mafft.cbrc.jp/alignment/software/) | [*Anolis carolinensis* genome](https://www.ncbi.nlm.nih.gov/genome/?term=Anolis+carolinensis)
