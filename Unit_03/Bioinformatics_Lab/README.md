# Bioinformatics Laboratory 3
>You will need a Unix Command Terminal or PuTTY interface to complete this lab. 

**Overvew**

To identify UCEs from targeted sequence capture data there are five main steps:

1. Clean raw FASTQ files for quality and adpater contamination.
2. Organise raw data by individuals/species
3. *de novo* assemble contigs using a stringent coverage level (e.g. 10X)
4. Identify contigs that include UCEs from each individual/species
5. Sort UCEs into appropriate directories
>For phylogenetic analyses etc., UCEs can then be aligned across all species/individuals. 

## Processing UCE data with phyluce

<details>
  <summary>Click to expand content!</summary>

>As we laready learned in [Unit 1](https://github.com/nhm-herpetology/museum-NGS-training/tree/main/Unit_01/Bioinformatics_Lab), phyluce is a really helpful program for processing targeted sequence capture data. There are seveal tutorials avialable here [here](https://phyluce.readthedocs.io/en/latest/tutorials/index.html)


2. Navigate to the SRA tools directory from [Unit 1](https://github.com/nhm-herpetology/museum-NGS-training/tree/main/Unit_01/Bioinformatics_Lab). We will download some raw data from three more snake species from the Streicher & Wiens [2016](https://www.sciencedirect.com/science/article/abs/pii/S1055790316300495?via%3Dihub) dataset; *Xenodermus javanicus*, *Micrurus fulvius*, and *Loxocemus bicolor*.

```
./fasterq-dump SRR3284492	
```
```
./fasterq-dump SRR3284197	
```
```
./fasterq-dump SRR3284196		
```
  
3. Now, we will move these new files to our phyluce directory from [Unit 1](https://github.com/nhm-herpetology/museum-NGS-training/tree/main/Unit_01/Bioinformatics_Lab):

```
cp SRR3284492_1.fastq /home/jefs/NGS_course/Unit_1/Data/raw-fastq
```  
```
cp SRR3284492_2.fastq /home/jefs/NGS_course/Unit_1/Data/raw-fastq
```   
```
cp SRR3284197_1.fastq /home/jefs/NGS_course/Unit_1/Data/raw-fastq
```  
```
cp SRR3284197_2.fastq /home/jefs/NGS_course/Unit_1/Data/raw-fastq
```    
```
cp SRR3284196_1.fastq /home/jefs/NGS_course/Unit_1/Data/raw-fastq
```  
```
cp SRR3284196_2.fastq /home/jefs/NGS_course/Unit_1/Data/raw-fastq
```     

4. Now navigate to the 'Data/raw-fastq' directory. Let's prepare the files for cleaning by renaming them and compressing them: 
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
  
1. Download the Tertrapod 5k probe sequences (this will be used to identify UCEs from the capture data). The probe set can also be downloaded [here](https://www.ultraconserved.org/)
  
```
wget https://raw.githubusercontent.com/nhm-herpetology/museum-NGS-training/main/Unit_03/Bioinformatics_Lab/Tetrapods-UCE-5Kv1.fasta
``` 
  
</details>

## Preparing UCE data for phylogenetic analysis

<details>
  <summary>Click to expand content!</summary>

>There is a really nice tutorial for assembling UCE data woth phyluce available [here](https://phyluce.readthedocs.io/en/latest/tutorials/tutorial-1.html). We will continue working with some of the squamate examples from before.
  
```
cd some_directory
```
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
>[UCEs](https://www.ultraconserved.org/) | [phyluce](https://phyluce.readthedocs.io/en/latest/) | [*Anolis carolinensis* genome](https://www.ncbi.nlm.nih.gov/genome/?term=Anolis+carolinensis)
