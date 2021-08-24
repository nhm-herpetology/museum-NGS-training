# Bioinformatics Laboratory 2

>You will need a Unix Command Terminal or PuTTY interface to complete this lab.

## *de novo* assembly of shotgun libraries

<details>
 <summary>Click to expand content!</summary>
 
>There are several different ways to assemble contigs from your raw Illumina data. In this lab we will compare two different assemblers. 

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
 
3. Using the Cylindrophis ruffus sample from [Unit 1](inser link) let's run velvet:
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


