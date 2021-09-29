# Bioinformatics Laboratory 4
>You will need a Unix Command Terminal or PuTTY interface to complete this laboratory. 

## Preparing raw ddRADseq data for processing using Stacks

<details>
  <summary>Click to expand content!</summary>
  
>Data will come back from the Illumina sequencer as demultiplexed by ddRADseq PCR 1 index. It will be demultiplexed using the bcl2fastq software we disussed in [Unit 1](https://github.com/nhm-herpetology/museum-NGS-training/tree/main/Unit_01/Bioinformatics_Lab). Following this, we will still need to sort each PCR index into FASTQ files for each of the individuals contained within the pool. We can do that using the software [Stacks](https://catchenlab.life.illinois.edu/stacks/) and a helpful program called ```process_radtags```

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

3. Let's make some working directories: 
```
mkdir raw
```
```
mkdir samples
```
```
mkdir stacks
```     
  
4. Now let's download some empirical data to analyze. We will use Index 5 of the *Craugastor augusti* ddRADseq data from Streicher et al. [2014](https://onlinelibrary.wiley.com/doi/abs/10.1111/mec.12814) that is used in the first module of the Unit 4 [Molecular Lab](https://github.com/nhm-herpetology/museum-NGS-training/tree/main/Unit_04/Molecular_Lab). 
  
Here is a SharePoint link that the course participants can use to download the demultiplexed file:  
  
[Craugastor_index_5_8bp_trim](https://naturalhistorymuseum.sharepoint.com/:u:/s/Herpetology/Eddrp3h57rJIr53ScPz34zEB5NcQQjd2oQOsK_YbJHT0pw?e=6U4VL8)  
  
This file is ~3.6 GB in size, so it will take several minutes to download. 

>Note: This file has already had the 8 Unique Molecular Identifier (UMI) nucleotides trimmed off, so it starts with the adapter index/barcode. I used [FastX Toolkit](https://github.com/agordon/fastx_toolkit) to trim the FASTQ file that was demultiplexed from teh Illumina HiSeq.  
  
5. The individual samples contained in the file are: 
  
Sample ID | Adapter Index/Barcode | PCR Index/Barcode
------------ | -------------  | -------------
MF 4398 | Index 1 (ACTAGG) | Index 5 (ACAGTG)
MF 5085 | Index 2 (GACCAA) | Index 5 (ACAGTG)
MF 6101 | Index 3 (TGTTGG)  | Index 5 (ACAGTG)
MF 6115 | Index 4 (CGAAAC)  | Index 5 (ACAGTG)
MF 6203 | Index 5 (AGCATT) | Index 5 (ACAGTG)
MF 6205 | Index 6 (CATCTC) | Index 5 (ACAGTG)
MVZ 226838 | Index 7 (GTCTAT) | Index 5 (ACAGTG) 
MVZ 226839 |Index 8 (TGGGAT) | Index 5 (ACAGTG)
JAC 30517 | Index 9 (TCTGCT) | Index 5 (ACAGTG)  
ENS 9494 | Index 10 (AACGGT)  | Index 5 (ACAGTG)   

We need to demultiplex them from the PCR primer index pool, so let's make a file called ```barcodes``` that we will use as a configuration file for the Stacks ```process_radtags``` command: 
  
 ```
 cat > barcodes
 ``` 
Paste the following text:
  
 ```
ACTAGG
GACCAA
TGTTGG
CGAAAC
AGCATT
CATCTC
GTCTAT
TGGGAT
TCTGCT
AACGGT
 ```  
>Now press CTRL + SHIFT + D to create the file.    
 
6. Now we run the ```process_radtags``` program using the following command: 
  
```  
process_radtags -f ./raw/index_1/trimmed/Craugastor_index_1_8bp_trim -o ./samples/ -b ./barcodes -c -q -r -e sbfI 
``` 
>This will perform a seond round of demultiplexing and place FASTQ files for each individual in the ```samples``` directory. 

7. Now we will modify the file names to match the sample IDs:

```   
cd samples
```  
  
```   
mv sample_AACGGT.fq ENS_9494.fq
mv sample_ACTAGG.fq MF_4398.fq
mv sample_AGCATT.fq MF_6203.fq
mv sample_CATCTC.fq MF_6205.fq
mv sample_CGAAAC.fq MF_6115.fq
mv sample_GACCAA.fq MF_5085.fq
mv sample_GTCTAT.fq MVZ_226838.fq
mv sample_TCTGCT.fq JAC_30517.fq
mv sample_TGGGAT.fq MVZ_226839.fq
mv sample_TGTTGG.fq MF_6101.fq
```
```   
cd ..
```   
  
>The files are now ready for downstream analysis and 'stacking'. More information is available in the Stacks [manual](https://catchenlab.life.illinois.edu/stacks/manual/), including some tutorials. 
  
  </details>

## Processing ddRADseq data from the SRA using Stacks

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

2. Move all of the FASTQ files to your ```Unit_4``` directory:

```  
mv *.fastq /home/jefs/NGS_course/Unit_4/  
```
>Reminder: your user name will need to be swapped with mine for this command to work

3. Now navigate to your ```Unit_4``` directory and check the format on the read 1 data: 
  
```  
head -3 SRR1947265_1.fastq
```  

We should see this printed:

```   
@SRR1947265.1 1_1101_2776_1933 length=89
AATGGGCGGCATATAAATATTTTAAATAAATAATAAAAATAAGATGGCAAGGTGGGAGAAGAGAGCAAGGAAGTGACTGATAGCAGAGA
+SRR1947265.1 1_1101_2776_1933 length=89
EDHGIGIIIIIIIEFHHIIGDDDEHHGHIIECEAEHGHFBEFFECEEC@ABB>ABB??=ACCCCBACCCCBAA4>C@CCCC@>ACC?A<
@SRR1947265.2 1_1101_2776_1974 length=89
AGGGATTGGACAAGGGTCTCTCTCCCAATACGTTGAGGAGGAAGGTAGCAGCCCTAGCATCGGTAATAAATTGGAAGGGATACAAATCT
+SRR1947265.2 1_1101_2776_1974 length=89
IIJJIGHJJIJJIIIIGHGHIJIJJJJJGIJJFCGGHGGHHHHHF;BEECEEDDDDDDDDCDDBA@DEDDEED:@CDDCDC<CCDDDDC
@SRR1947265.3 1_1101_4980_1990 length=89
CCACTTAGAGAGGGCTGTAAAGCAGTATATACGTCTATCTACTATTGACATTTCAATATTTTAATCCGTATAATTTTAATGTGTTATTT
  @SRR1947265.1 1_1101_2776_1933 length=89
AATGGGCGGCATATAAATATTTTAAATAAATAATAAAAATAAGATGGCAAGGTGGGAGAAGAGAGCAAGGAAGTGACTGATAGCAGAGA
+SRR1947265.1 1_1101_2776_1933 length=89
EDHGIGIIIIIIIEFHHIIGDDDEHHGHIIECEAEHGHFBEFFECEEC@ABB>ABB??=ACCCCBACCCCBAA4>C@CCCC@>ACC?A<
@SRR1947265.2 1_1101_2776_1974 length=89
AGGGATTGGACAAGGGTCTCTCTCCCAATACGTTGAGGAGGAAGGTAGCAGCCCTAGCATCGGTAATAAATTGGAAGGGATACAAATCT
+SRR1947265.2 1_1101_2776_1974 length=89
IIJJIGHJJIJJIIIIGHGHIJIJJJJJGIJJFCGGHGGHHHHHF;BEECEEDDDDDDDDCDDBA@DEDDEED:@CDDCDC<CCDDDDC
@SRR1947265.3 1_1101_4980_1990 length=89
CCACTTAGAGAGGGCTGTAAAGCAGTATATACGTCTATCTACTATTGACATTTCAATATTTTAATCCGTATAATTTTAATGTGTTATTT
``` 
  
4. Now let's do the same for an example read 2 file:   

```  
head -10 SRR1947265_2.fastq
```    

We should see this printed:

```   
@SRR1947265.1 1_1101_2776_1933 length=97
TCCTCTAGGACTGGCCGGTTTGATCGCTTTGCAGTCCAAAGGACTCGCAAAATCTTAGCCTTGCACTAAATGCATATCCTTATATTTTCTTTTATTC
+SRR1947265.1 1_1101_2776_1933 length=97
HIEBHEIIIIGCHIIIII@DDFIBF;FHIFGCAC=C>ADHFEEG@>EEFFDECACCD@CCDCDDCCDDDDDD@C<A@C>>@@ACCDEECCCD@CDDE
@SRR1947265.2 1_1101_2776_1974 length=97
TTTTCTGACTGAAAGGGCTGCCAATTCAGACACTCTGCGGGCAGATGTGATTGCCACCAGGAAGGCCACTTTATATGAAAGAAGATGGAGACTAATA
+SRR1947265.2 1_1101_2776_1974 length=97
GJIIJJJJJJJJJJIIGHGHIJJIGHIJIIJJJGJGICHIIJHHFFFFFDEDEEEDDDDBBDBBBBB<@CDCDDEEEEEDDDBCCDDDC89?@CCCD
@SRR1947265.3 1_1101_4980_1990 length=97
CCTCTTGCAGATATCCTTATGTCGCAGCTGTGGTCTCCCTCTAGGGCATCCATTCCTTACAAAAGTCGTTTCATAATGTCATTGAATAATGACAAAG
``` 

>These datasets seem to have been cleaned already so that they can be placed directly into the ```samples```  directory. 
  
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
