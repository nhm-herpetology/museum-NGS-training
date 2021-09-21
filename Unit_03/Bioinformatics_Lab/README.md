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
  
4. Before we run illumiprocessor, let's remove the ```clean-fastq``` directory and ```illumiprocessor.conf``` file from [Unit 1](https://github.com/nhm-herpetology/museum-NGS-training/tree/main/Unit_01/Bioinformatics_Lab):
  
```
rm -r clean-fastq
```
```
rm illumiprocessor.conf
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
    --cores 1  
 ```   
 
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
>Now we are ready to identify which contigs correspond to UCE loci. 
  
11. Download the Tetrapod 5k probe sequences (this will be used to identify UCEs from the capture data). The probe set can also be downloaded [here](https://www.ultraconserved.org/)
  
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
