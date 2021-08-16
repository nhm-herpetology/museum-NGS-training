# Computer Laboratory 3
>You will need a Unix Command Terminal or PuTTY interface to complete this lab. 

**Overvew**

To identify UCEs from targeted sequence capture data there are five main steps:

1. Clean raw FASTQ files for quality and adpater contamination.
2. Organise raw data by individuals/species
3. *de novo* assemble contigs using a stringent coverage level (e.g. 10X)
4. Identify contigs that include UCEs from each individual/species
5. Sort UCEs into appropriate directories
>For phylogenetic analyses, UCEs can then be aligned across all species/individuals for downstream applications. 

## Processing UCE data with phyluce

<details>
  <summary>Click to expand content!</summary>

>Phyluce is a really helpful program for processing targeted sequence capture data. There are seveal tutorials avialable here [here](https://phyluce.readthedocs.io/en/latest/tutorials/index.html)


Example datasets: 

* Illumina HiSeq (download here)
* Illumina MiSeq (download here)




```
cd some_directory
```

**Helpful Links**
>[velvet](https://www.ebi.ac.uk/~zerbino/velvet/) | [phyluce](https://phyluce.readthedocs.io/en/latest/)
