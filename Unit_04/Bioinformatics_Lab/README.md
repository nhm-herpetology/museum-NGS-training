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
mkdir samples-frogs
```
```
mkdir stacks-frogs
```     
  
4. Now let's download some empirical data to analyze. We will use Index 5 of the *Craugastor augusti* ddRADseq data from Streicher et al. [2014](https://onlinelibrary.wiley.com/doi/abs/10.1111/mec.12814) that is used in the first module of the Unit 4 [Molecular Lab](https://github.com/nhm-herpetology/museum-NGS-training/tree/main/Unit_04/Molecular_Lab). 
  
Here is a SharePoint link that the course participants can use to download the demultiplexed file:  
  
[Craugastor_index_5_8bp_trim](https://naturalhistorymuseum.sharepoint.com/:u:/s/Herpetology/Eddrp3h57rJIr53ScPz34zEB5NcQQjd2oQOsK_YbJHT0pw?e=6U4VL8)  
  
This file is ~3.6 GB in size, so it will take several minutes to download. 

>Note: This file has already had the 8 Unique Molecular Identifier (UMI) nucleotides trimmed off, so it starts with the adapter index/barcode. I used [FastX Toolkit](https://github.com/agordon/fastx_toolkit) to trim the FASTQ file that was demultiplexed from teh Illumina HiSeq.  
 
5. Let's have a look at the first few lines of the 'PCR Index 5' FASTQ file: 

```  
cd raw
``` 
```  
head -10 Craugastor_index_5_8bp_trim
```
We should see: 
```  
CGAAACTGCAGGTTCTTTGGGTTCCACTTCCCGTTTAGACCTGGCCGGCATTCTTCTGGATCATCCTGAGGGAAAGGCTGCTTGACCAGCAG
+HWI-ST594:2:1101:1372:2234#ACAGTGACAGTG/1
cgc`echhhhhhhf[^[e[c`afQIOIO^`fBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB
@HWI-ST594:2:1101:1693:2240#ACAGTGACAGTG/1
GACCAATGCAGGCACCACAGACACCTGGTAGCTACTGATAACCATCATAGTTCTGGAGCAATGATCTGGGCCCACCTCTGCAGACCACACCA
+HWI-ST594:2:1101:1693:2240#ACAGTGACAGTG/1
gggggihgfhghihiiiihiiihhiiiigiiiiiiiiihiifhfhhhhhhihiiihhifagdgdgggeeeecccccccccccbccabaccac
@HWI-ST594:2:1101:1995:2249#ACAGTGACAGTG/1
TGTTGGTGCAGATAGGCAACACATGCCCCTGTTGGGAATACCTCTTTAAAGCGATGCTCTGGTTTCGGGATGAAATTCTCTCCTGACTGGAG
```
>Note that the barcodes (listed below) for multiple individuals appear first, followed by the 'ACTG' SbfI cutsite remnant.   
  
6. The individual samples contained in the file are: 
  
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
 cd ..
 ```   
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
>Now press ENTER then CTRL + SHIFT + D to create the file.    
 
7. Now we run the ```process_radtags``` program using the following command: 
  
```  
./process_radtags -f ./raw/Craugastor_index_5_8bp_trim -o ./samples-frogs/ -b ./barcodes -c -q -r -e sbfI 
``` 
>This will perform a seond round of demultiplexing and place FASTQ files for each individual in the ```samples``` directory. It should take ~4 minutes to run. For definitions of ```process_radtags``` commands click [here](https://catchenlab.life.illinois.edu/stacks/comp/process_radtags.php) 

8. Now we will modify the file names to match the sample IDs:

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
mv *.fastq /home/jefs/NGS_course/Unit_4/stacks-2.59  
```
>Reminder: your user name will need to be swapped with mine for this command to work

3. Now navigate to your ```Unit_4/stacks-2.59``` directory and check the format on the read 1 data: 
  
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

5. Now we need to make our working directories for Stacks. These datasets seem to have been cleaned already so that they can be placed directly into the ```samples-snakes```  directory. 
                                                                                                  
```
mkdir samples-snakes
```   
                                                                                                  
```
mkdir stacks-snakes
```                                                                                                  
                                                                                                  
```
mv *fastq samples-snakes
```

6. Rename the files so that they are easier to work with: 

```
cd samples-snakes  
```  
  
```
mv SRR1947266_1.fastq M86_fulvius_1.fastq
mv SRR1947266_2.fastq M86_fulvius_2.fastq
mv SRR1947265_1.fastq M87_fulvius_1.fastq  
mv SRR1947265_2.fastq M87_fulvius_1.fastq
mv SRR1947267_1.fastq M692_fulvius_1.fastq
mv SRR1947267_2.fastq M692_fulvius_2.fastq 
mv SRR1947271_1.fastq M206_tener_1.fastq  
mv SRR1947271_2.fastq M206_tener_2.fastq    
mv SRR1947351_1.fastq M230_tener_1.fastq 
mv SRR1947351_2.fastq M230_tener_2.fastq 
mv SRR1947349_1.fastq M279_tener_1.fastq 
mv SRR1947349_2.fastq M279_tener_2.fastq   
```   

```
cd ..  
```                                                                                                 
                                                                                                  
7. We will now run USTACKS which is a Stacks program that takes a set of short-read sequences and align them into exactly-matching stacks (or putative alleles). Comparing the stacks it will form a set of putative loci and detect SNPs at each locus using a maximum likelihood framework. For definitions of USTACKS ommands click [here](https://catchenlab.life.illinois.edu/stacks/comp/ustacks.php).
                                                                                                  
```
./ustacks -f ./samples-snakes/M86_fulvius_1.fastq -o ./stacks-snakes -i 1 -m 3 -M 4 -p 16
./ustacks -f ./samples-snakes/M87_fulvius_1.fastq -o ./stacks-snakes -i 2 -m 3 -M 4 -p 16
./ustacks -f ./samples-snakes/M692_fulvius_1.fastq -o ./stacks-snakes -i 3 -m 3 -M 4 -p 16
./ustacks -f ./samples-snakes/M206_tener_1.fastq -o ./stacks-snakes -i 4 -m 3 -M 4 -p 16
./ustacks -f ./samples-snakes/M230_tener_1.fastq -o ./stacks-snakes -i 5 -m 3 -M 4 -p 16                                                                                         
./ustacks -f ./samples-snakes/M279_tener_1.fastq -o ./stacks-snakes -i 6 -m 3 -M 4 -p 16                                                                                         
```                                                                                                  
>There should now be individual stacks files in the ```stacks-snakes``` directory.                                                                                               
   
8. We will now run CSTACKS which is a Stacks program that creates a set of consensus loci, merging alleles together that are listed in the USTACKS output. First, we need to make a 'population map' that will be used to identify the individuals we want to process in CTACKS: 
  
```
cat > config_individuals.txt
```  
 
Paste the following text: 
```
M86_fulvius_1       1
M87_fulvius_1       2
M692_fulvius_1      3
M206_tener_1        4
M230_tener_1        5 
M279_tener_1        6
```    
Now press CTRL + SHIFT + D to create the file.
  
9. Run CSTACKS using the following command: 
  
```
./cstacks -P ./stacks-snakes -M ./config_individuals.txt -n 4 -p 15  
```  
>For definitions of CSTACKS commands click [here](https://catchenlab.life.illinois.edu/stacks/comp/cstacks.php)
  
10. Next we will run the Stacks program SSTACKS. Sets of stacks, i.e. putative loci, constructed by the USTACKS program can be searched against a catalog produced by CSTACKS. In the case of a general population, all samples in the population would be matched against the catalog with SSTACKS. For definitions of SSTACKS commands click [here](https://catchenlab.life.illinois.edu/stacks/comp/sstacks.php)  
 
```
./sstacks -P ./stacks-snakes -M ./config_individuals.txt -p 8 
```   

11. Next we will run the Stacks program TSV2BAM. The TSV2BAM program will transpose data so that it is oriented by locus, instead of by sample. For definitions of TSV2BAM commands click [here](https://catchenlab.life.illinois.edu/stacks/comp/tsv2bam.php)   
  
```
./tsv2bam -P ./stacks-snakes/ -M ./config_individuals.txt -t 8 
```    

12. Finally. we will run the Stacks program GSTACKS. GSTACKS will identify SNPs within the meta population for each locus and then genotype each individual at each identified SNP. Once SNPs have been identified and genotyped, gstacks will phase the SNPs at each locus, in each individual, into a set of haplotypes. For definitions of GSTACKS commands click [here](https://catchenlab.life.illinois.edu/stacks/comp/gstacks.php)
  
```
./gstacks -P ./stacks-snakes -M ./config_individuals.txt -t 8
```   
>Your RADseq data are now ready for analysis and output using the ```populations``` program discussed in teh next module.  
  
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
