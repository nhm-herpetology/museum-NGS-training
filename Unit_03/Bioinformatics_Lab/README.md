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

>Phyluce is a really helpful program for processing targeted sequence capture data. There are seveal tutorials avialable here [here](https://phyluce.readthedocs.io/en/latest/tutorials/index.html)

1. Download the Tertrapod 5k probe sequences (this will be used to identify UCEs from the capture data). The probe set can also be downloaded [here](https://www.ultraconserved.org/)
  
```
wget https://github.com/nhm-herpetology/museum-NGS-training/blob/main/Unit_03/Bioinformatics_Lab/Tetrapods-UCE-5Kv1.fasta
```

2. Next we will download some raw data from the NCBI SRA.
```
wget https://github.com/nhm-herpetology/museum-NGS-training/blob/main/Unit_03/Bioinformatics_Lab/Tetrapods-UCE-5Kv1.fasta
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

1. We should have the NCBI Entrez Direct UNIX E-utilities installed from the [Unit 2](XXX) bioinformatics lab. so that we can download genomic sequences 
  
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
mv NC_014781.1 /home/jefs/NGS_course/Unit_3
```
  
  
  
</details>


**Helpful Links**
>[velvet](https://www.ebi.ac.uk/~zerbino/velvet/) | [phyluce](https://phyluce.readthedocs.io/en/latest/)
