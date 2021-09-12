# Bioinformatics Laboratory 2

>You will need a Unix Command Terminal or PuTTY interface to complete this lab.

## *de novo* assembly of libraries using phyluce

<details>
 <summary>Click to expand content!</summary>

 >There are several different ways to assemble contigs from your cleaned Illumina FASTQ data. In this module we will compare the results of two different assemblers that we will execute in [phyluce](https://phyluce.readthedocs.io/en/latest/index.html).

1. We will use the three sets of cleaned fastq.gz files from [Unit 1](https://github.com/nhm-herpetology/museum-NGS-training/tree/main/Unit_01/Bioinformatics_Lab) that were downloaded from the NCBI [SRA](https://www.ncbi.nlm.nih.gov/sra) and originally sequenced for Streicher & Wiens ([2016](https://www.sciencedirect.com/science/article/abs/pii/S1055790316300495?via%3Dihub)).  
```  
Cylindrophis_ruffus_FMNH_258674-READ1.fastq.gz
Cylindrophis_ruffus_FMNH_258674-READ2.fastq.gz
Cylindrophis_ruffus_FMNH_258674-READ-singleton.fastq.gz
```  
 
</details>

 ## Comparing kmer sizes  and coverage depths of *de novo* assemblies using velvet

<details>
 <summary>Click to expand content!</summary>
 
>As we discussed in lecture earlier today, different kmer lengths and coverge thresholds produce different assembly results. We will see examples of this by generating a handful of assemblies in [velvet](https://www.ebi.ac.uk/~zerbino/velvet/). 

1. First let's download velvet 1.2.10: 
 ```
wget https://www.ebi.ac.uk/~zerbino/velvet/velvet_1.2.10.tgz
```

2. Now let's unzip and make the software: 
``` 
tar -xvzf velvet_1.2.10.tgz
```
``` 
rm velvet_1.2.10.tgz
```
```
cd velvet_1.2.10
```
``` 
make 'MAXKMERLENGTH=127' 
``` 
>This should make two executable files ```velveth``` and ```velvetg```

3. You should have three sets of cleaned fastq.gz files from [Unit 1](https://github.com/nhm-herpetology/museum-NGS-training/tree/main/Unit_01/Bioinformatics_Lab)  
```  
Cylindrophis_ruffus_FMNH_258674-READ1.fastq.gz
Cylindrophis_ruffus_FMNH_258674-READ2.fastq.gz
Cylindrophis_ruffus_FMNH_258674-READ-singleton.fastq.gz
```  
 
4. Using the Cylindrophis ruffus sample from [Unit 1](https://github.com/nhm-herpetology/museum-NGS-training/tree/main/Unit_01/Bioinformatics_Lab), let's run velvet using the default kmer size:
```
./velveth output_directory/ 48 -fasta -short solexa1.fa solexa2.fa solexa3.fa -long capillary.fa
``` 
5. Now let's run velvet using the largest possible kmer size:
 ```
./velveth output_directory/ 127 -fasta -short solexa1.fa solexa2.fa solexa3.fa -long capillary.fa
``` 


</details>

## Reference sequence mapping

<details>
 <summary>Click to expand content!</summary>
 
>Reference-based assemblies can be useful when you have low coverage data (e.g. museum specimen shotgun sequencing) and a good reference genome.  

```
cd some_directory
```

</details>

**Helpful Links** 
> [velvet](https://www.ebi.ac.uk/~zerbino/velvet/) | [Spades](https://cab.spbu.ru/software/spades/) |[BWA](https://github.com/lh3/bwa) | [WinSCP](https://winscp.net/eng/download.php) | [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) 

