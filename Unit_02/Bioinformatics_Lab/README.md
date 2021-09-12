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
>These files should be inside a directory called ```Unit_1/Data/clean-fastq/Cylindrophis_ruffus_FMNH_258674/split-adapter-quality-trimmed```
 
2. Activate phyluce
 ```  
  conda activate phyluce-1.7.1
 ``` 
3. To use phyluce to assemble reads into contigs, a configuration file is needed. The configuration file looks like this:

```
[samples]
Cylindrophis_ruffus_FMNH_258674:clean-fastq/Cylindrophis_ruffus_FMNH_258674/split-adapter-quality-trimmed/
  
```
The configuration file tells phyluce where to find the files that are to be *de novo* assembled. Our example only contains one sample, but you can have configuration files with as many samples/taxa/individuals as you like.

4. To make the configuration text file let's use the command line: 
 
 ```  
  cat > assembly.conf
 ```   
 Now paste the configuration text (from Step 3) into your terminal and then press CTRL + SHIFT + D. 
 
5. We are now ready to assemble the reads into contigs using velvet: 
 ```   
phyluce_assembly_assemblo_velvet \
    --conf assembly.conf \
    --output velvet-assemblies \
    --cores 12 
 ```
 >This will place the ouput files in a new directory called velvet-assemblies. On Franklin it should take about 3 mins to run. 
 
 6. Next, let's use the same configuration file to assemble the reads into contigs using spades: 
 ```   
phyluce_assembly_assemblo_spades \
    --conf assembly.conf \
    --output spades-assemblies \
    --cores 12 
 ``` 
  >This will place the ouput files in a new directory called spades-assemblies. On Franklin this may take ~10 mins to run.  

Once both assemblies have finished our ```Data``` directory should contain the following items: 
 
```
 assembly.conf         illumiprocessor.log                   raw-fastq
clean-fastq           phyluce_assembly_assemblo_spades.log  spades-assemblies
illumiprocessor.conf  phyluce_assembly_assemblo_velvet.log  velvet-assemblies
```

7. First, let's look at the velvet assembly:

```
cd velvet-assemblies
``` 
>There should be two directories ```contigs``` and  ```Cylindrophis_ruffus_FMNH_258674```
 
8. The ```contigs``` directory contains a single FASTA file which is the output of the assembly. It will contain hundreds to thousands of sequences inferred by the assembly. 
 
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

