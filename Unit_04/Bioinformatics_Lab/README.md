# Bioinformatics Laboratory 4
>You will need a Unix Command Terminal or PuTTY interface to complete this laboratory. 

## Preparing ddRADseq data for processing using Stacks

<details>
  <summary>Click to expand content!</summary>
  
>Data will come back from the Illumina sequenceer as demultiplexed by the PCR index. We will need to sort each PCR index into datasets for each of the individuals contained within it. We can do that using a helpful script called ```process_radtags```

1. First, let's make a new directory inside ```NGS_course``` called ```Unit_4```

```
cd NGS_course
```
```
mkdir Unit_4
```  
```
cd Unit_4
```    
  
2. Let's download and install Stacks 2.59:

```
wget https://catchenlab.life.illinois.edu/stacks/source/stacks-2.59.tar.gz
```
```
tar xfvz stacks-2.59.tar.gz
```  
```
cd stacks-2.59
``` 
```
./configure
```
```
make
```  
>The installation may take ~2-5 minutes
  
3. Now let's download some empirical data to analyze. Navigate to the SRA toolkit folder from [Unit 1](https://github.com/nhm-herpetology/museum-NGS-training/tree/main/Unit_01/Bioinformatics_Lab). 
  
  
>More information is available in the Stacks [manual](https://catchenlab.life.illinois.edu/stacks/manual/), including some tutorials. 
  </details>

## Processing ddRADseq data using Stacks

<details>
  <summary>Click to expand content!</summary>
  
>Description will go here.
Example datasets: 

* Illumina HiSeq (download here)
* Illumina MiSeq (download here)


```
cd some_directory
```  
  </details>

## Processing ddRADseq data using dDocent

<details>
  <summary>Click to expand content!</summary>
  
>Description will go here.
Example datasets: 

* Illumina HiSeq (download here)
* Illumina MiSeq (download here)


```
cd some_directory
```  
  </details>

**Helpful Links**
>[Stacks](https://catchenlab.life.illinois.edu/stacks/) | [dDocent](https://www.ddocent.com/) | [ipyrad](https://ipyrad.readthedocs.io/en/master/)
