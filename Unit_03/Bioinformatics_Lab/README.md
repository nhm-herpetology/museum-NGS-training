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

```
cd some_directory
```
</details>

## Mapping UCE data to genomic assemblies

<details>
  <summary>Click to expand content!</summary>

>Aligning UCEs (or any locus) to genomic assemblies is helpful for assessing linkage

We will use the vertebrate 5k UCE probe sequences in FASTA format available [here](insert link), and an example of mapping these UCEs on chromosomes 6 (80.74 Mbp) of *Anolis carolinensis*  

1. Let's install the NCBI Entrez Direct UNIX E-utilities so that we can download genomic sequences 
  
```
wget https://www.ncbi.nlm.nih.gov/books/NBK179288/bin/install-edirect.sh
```
</details>


**Helpful Links**
>[velvet](https://www.ebi.ac.uk/~zerbino/velvet/) | [phyluce](https://phyluce.readthedocs.io/en/latest/)
