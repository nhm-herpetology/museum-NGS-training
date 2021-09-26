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
  
>We will explore Stacks using some data from North American coralsnakes generated for Streicher et al. [2016](https://onlinelibrary.wiley.com/doi/10.1111/evo.12967). We will download data from 3 individuals for *Micrurus tener* and 3 individuals of *Micrurus fulvius*. 
  
1. Navigate to the SRA toolkit folder from [Unit 1](https://github.com/nhm-herpetology/museum-NGS-training/tree/main/Unit_01/Bioinformatics_Lab). 

```
./fasterq-dump SRR1947266
```  
>These are ddRADseq data from *M. fulvius* M86 from Tampa, Florida, USA. The download should take 1-2 minutes.   

```
./fasterq-dump SRR1947265
```  
>These are ddRADseq data from *M. fulvius* M87 from Walton, Florida, USA. The download should take 1-2 minutes.   

```
./fasterq-dump SRR1947267 
```  
>These are ddRADseq data from *M. fulvius* M692 from New Hanover, North Carolina, USA. The download should take 2-3 minutes.     

```
./fasterq-dump SRR1947271	 
```  
>These are ddRADseq data from *M. tener* M206 from Tamaulipas, Mexico. The download should take 2-3 minutes.    

```
./fasterq-dump SRR1947351	 
```  
>These are ddRADseq data from *M. tener* M230 from Anderson, Texas, USA. The download should take 1-2 minutes.  

```
./fasterq-dump SRR1947349		 
```  
>These are ddRADseq data from *M. tener* M279 from Brazos, Texas, USA. The download should take 1-2 minutes.     
  
  </details>

## Generating population genetic statistics in Stacks

<details>
  <summary>Click to expand content!</summary>
  
>We can generate summary statistics and population genetic statistics using the ```populations``` program from stacks and configuration files. Let's use the data we downloaded for the last module. 

1. First, let's summarise by species using the following configuration file (referred to as the 'population map' in Stacks manual):

```
M86       fulvius
M87       fulvius
M692      fulvius
M206      tener
M230      tener 
M279      tener
``` 

2. Let's make the configuration file:   
  
```
cat > config_species.txt
```  
Now paste the configuration text (from Step 1) into your terminal and then press CTRL + SHIFT + D.
  
  
3. Now let's treat each individual as a single entity. The configuration file (referred to as the 'population map' in Stacks manual) should be: 
  
```
M86       1
M87       2
M692      3
M206      4
M230      5 
M279      6
```  
  
4. Let's make the configuration file:   
  
```
cat > config_individuals.txt
```  
Now paste the configuration text (from Step 3) into your terminal and then press CTRL + SHIFT + D.  
  
5. Run the ```populations``` program using the first configuration file: 

```
populations -P ./stacks/ --popmap ./samples/config_species.txt --smooth -p 10 -r 0.75 -f p_value -t 8 --structure --genepop --write-single-snp   
```
  
6. Run the ```populations``` program using the second configuration file:   

```
populations -P ./stacks/ --popmap ./samples/config_individuals.txt --smooth -p 10 -r 0.75 -f p_value -t 8 --structure --genepop --write-single-snp   
```  
  
  
  </details>

**Helpful Links**
>[Stacks](https://catchenlab.life.illinois.edu/stacks/) | [dDocent](https://www.ddocent.com/) | [ipyrad](https://ipyrad.readthedocs.io/en/master/)
